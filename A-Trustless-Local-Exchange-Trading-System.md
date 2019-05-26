A Local Exchange Trading System (LETS) is aimed at developing local economy and is usually used by people of a locality in the vicinity of each other. A committee managed LETS is described at [this link](https://github.com/ergoplatform/ergo/wiki/A-Local-Exchange-Trading-System-On-Top-Of-Ergo). We call such a system a _managed_ or _permissioned_, since it depends on a trusted committee. Here we describe a **trustless** LETS system, i.e., one where there is no management committee. 

LETS involves several parties that agree to use some form of "local currency", usually pegged to the country's main currency at a 1:1 rate. Assume that our LETS is based in a European country where the currency is Euros, and the exchange is done in "local Euros", which are considered to be equivalent to national Euros.

Each user in LETS has an _account_, which contains the LETS balance of that user (in Local Euros). On joining, each user has a balance of zero. The balance is stored in a (possibly decentralized) ledger. An interesting feature of LETS is that a user with zero balance can also "withdraw" money, but only for paying another LETS user. At any time the sum of LETS balances of all the users is zero.

As an example, Alice with zero balance wishes to purchase one liter of milk for 2 Euros from Bob who is also a member of LETS with zero balance. She transfers 2 Euros from her account to Bob's, making her balance -2 and Bob's +2. Bob can then transfer some or all of his balance to another LETS user in exchange for goods or services. 

Since we desire a trustless LETS, we cannot depend on any trusted group of people to admit users. 
 
We will assume a _rate oracle_ identified by some global id and a singleton box containing exactly one token with this id. This box also contains the rate of Ergs to Euros at any given period of time. The rate is updated by spending this box and creating another singleton box with the new rate.

At any instance, our LETS is defined by a global _LETS token box_ that contains some LETS membership tokens. This box is protected by the script given below. The token ID uniquely defines the attributes of the LETS in use, such as the location, the currency unit, the rate oracle ID, etc. 
One or more users can spend this box and create their individual LETS boxes as outputs of the transaction. The box is initially started with, say, 10000 LETS membership tokens. 

A LETS box represents a LETS member and must be used for a LETS transaction. A LETS transaction is between two LETS members, one being the sender and the other the receiver, such that the sender transfers some positive amount of the LETS currency (local Euros) to the receiver. Such a transaction consumes the member's boxes and recreates them as output with the updated balance.   

To prevent spam and DDoS attacks, we require at least some minimum number of ergs (`minErgsToJoin`) to be locked in the newly created member's box. The ergs will be locked until at least `minWithdrawTime` number of blocks have been mined. A box is allowed to have a negative LETS balance upto the amount that can be covered by the locked ergs (using the rate at the time of trade). 

	val tokenBox = OUTPUTS(0) // first output should contain remaining LETS tokens
	def isLets(b:Box) = {
	   // A LETS box must have 1 membership token in tokens(0)
	   b.tokens(0)._1 == letsTokenID && b.tokens(0)._2 == 1 &&
	   blake2b256(b.propositionBytes) == memberBoxScriptHash &&
	   SELF.R4[Long].get == 0 && // start box with zero LETS balance
	   b.value >= minErgsToJoin && 
	   b.R6[Long].get <= HEIGHT // store the creation height in R6
	}
	val numLetsBoxes = OUTPUTS.filter({(b:Box) => isLets(b)}).size
	tokenBox.tokens(0)._1 == SELF.tokens(0)._1 &&
	tokenBox.tokens(0)._2 == SELF.tokens(0)._2 - numLetsBoxes

A LETS member's box is given by the script below, whose hash `memberBoxScriptHash` is used above.

	val validRateOracle = CONTEXT.dataInputs(0).tokens(0)._1 == rateTokenID
	val rate = CONTEXT.dataInputs(0).R4[Int].get
	val inBalance = SELF.R4[Long].get
	val pubKey = SELF.R5[SigmaProp].get
	val createdAt = SELF.R6[Long].get

	val index = getVar[Int](0).get
	val outBalance = OUTPUTS(index).R4[Long].get
	val isMemberBox = {(b:Box) => b.propositionBytes == SELF.propositionBytes}
	val letsInputs = INPUTS.filter(isMemberBox)
	val letsOutputs = OUTPUTS.filter(isMemberBox)

	// receiver box will contain same amount of ergs.
	val receiver = outBalance > inBalance && OUTPUTS(index).value == SELF.value
	val letsBalance = {(b:Box) => b.R4[Long].get}

	val letsIn = letsInputs.map(letsBalance).fold(0L, {(l:Long, r:Long) => l + r})
	val letsOut = letsOutputs.map(letsBalance).fold(0L, {(l:Long, r:Long) => l + r})

	// Sender box can contain less amount of ergs (sender may withdraw ergs 
	// provided that its negative LETS balance is backed by sufficient ergs
	// We don't touch the erg balance of the receiver

	val correctErgs = OUTPUTS(index).value >= -outBalance * rate && (
	  OUTPUTS(index).value >= SELF.value || 
	  SELF.R6[Long].get + minWithdrawTime > HEIGHT
	)

	inBalance != outBalance && // some transaction should occur
	SELF.tokens(0)._1 == letsTokenID &&
	OUTPUTS(index).tokens(0)._1 == letsTokenID &&
	validRateOracle && // rate oracle is valid
	letsIn == letsOut && // total LETS balance is preserved
	letsInputs.size == 2 && letsOutputs.size == 2 &&
	OUTPUTS(index).propositionBytes == SELF.propositionBytes &&
	OUTPUTS(index).R5[SigmaProp].get == pubKey &&
	OUTPUTS(index).R6[Long].get == SELF.R6[Long].get && // creation height
	(receiver || (pubKey && correctErgs))

The transaction spending a box with the above script requires:
- The sum of the LETS balance of inputs and outputs is preserved
- There are two LETS inputs and two LETS outputs
- The public keys (stored in R5) is preserved in the corresponding output
- The creation height (stored in R6) be preserved in the corresponding output

We say that some public key is the receiver if the LETS balance of its output is higher than that of its input. 

The last condition requires that either the input (and output) box belongs to the receiver (so that the number of Ergs are preserved), or the output is backed by the required number of Ergs if its LETS balance is negative. Furthermore, it requires that the sender's ergs balance cannot be reduced until `minWithdrawTime` number of blocks have been mined after the ergs were locked.