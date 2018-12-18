# Standard Library

# Types
|type|adds|
|-------|---|
| [Unit](#Unit) | Native |   
| <a>Int</a> | Native |   
|  <a>Boolean</a> | Native |   
| <a>ByteVector</a> | Native |   
| <a>String | Native |   
| <a>Address</a> |   <ul> <li> <b>bytes</b> <a> ByteVector </li></ul>|
| <a>Alias</a> |   <ul> <li> <b>alias</b> <a> String</li></ul>|
| [Transfer](#Transfer) |   <ul> <li> <b>recipient</b> <a>Address</a> <a>Alias </li> <li> <b>amount</b> <a>Int </li></ul>|
| [Order](#Order) |   <ul> <li> <b>id</b> <a> ByteVector </li> <li> <b>matcherPublicKey</b> <a>ByteVector </li> <li> <b>assetPair</b> <a>AssetPair </li> <li> <b>orderType</b> <a>Buy</a> <a>Sell </li> <li> <b>price</b> <a>Int </li> <li> <b>amount</b> <a>Int </li> <li> <b>timestamp</b> <a>Int </li> <li> <b>expiration</b> <a> Int </li> <li> <b>matcherFee</b> <a>Int </li> <li> <b>sender</b> <a>Address </li> <li> <b>senderPublicKey</b> <a>ByteVector </li> <li> <b>bodyBytes</b> <a>ByteVector </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</li></ul>|
| <a> AssetPair |   <ul> <li> <b>amountAsset</b> <a>OPTION(ByteVector)</li> <li> <b>priceAsset</b> <a>OPTION(ByteVector)</li></ul>|
| [DataEntry](#DataEntry) |   <ul> <li> <b>key</b> <a>String </li> <li> <b>value</b>  <a> Int </a> <a> Boolean </a> <a>ByteVector</a> <a>String </li></ul>|
| [Transaction](#Transaction) |    [TransferTransaction](#TransferTransaction) [IssueTransaction](#IssueTransaction) [ReissueTransaction](#ReissueTransaction) [BurnTransaction](#BurnTransaction) [LeaseTransaction](#LeaseTransaction) [LeaseCancelTransaction](#LeaseCancelTransaction) [MassTransferTransaction](#MassTransferTransaction) [CreateAliasTransaction](#CreateAliasTransaction) [SetScriptTransaction](#SetScriptTransaction) [SponsorFeeTransaction](#SponsorFeeTransaction) [ExchangeTransaction](#ExchangeTransaction) [DataTransaction](#DataTransaction)
| [GenesisTransaction](#GenesisTransaction) |   <ul> <li> <b>amount</b> <a>Int</a> </li> <li> <b>recipient</b><a>Address</a> <a>Alias</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li></ul>|
| [PaymentTransaction](#PaymentTransaction) |   <ul> <li> <b>amount</b> <a>Int</a> </li> <li> <b>recipient</b><a>Address</a> <a>Alias</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [TransferTransaction](#TransferTransaction) |   <ul> <li> <b>feeAssetId</b> <a>OPTION(ByteVector)</li> <li> <b>amount</b> <a>Int</a> </li> <li> <b>assetId</b> <a>OPTION(ByteVector)</li> <li> <b>recipient</b><a>Address</a> <a>Alias</a> </li> <li> <b>attachment</b> <a>ByteVector</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [IssueTransaction](#IssueTransaction) |   <ul> <li> <b>quantity</b> <a>Int</a> </li> <li> <b>name</b> <a>ByteVector</a> </li> <li> <b>description</b> <a>ByteVector</a> </li> <li> <b>reissuable</b>  <a>Boolean</a> </li> <li> <b>decimals</b> <a>Int</a> </li> <li> <b>script</b>  <a>OPTION(ByteVector)</a></li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [ReissueTransaction](#ReissueTransaction) |   <ul> <li> <b>quantity</b> <a>Int</a> </li> <li> <b>assetId</b> <a>ByteVector</a> </li> <li> <b>reissuable</b>  <a>Boolean</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [BurnTransaction](#BurnTransaction) |   <ul> <li> <b>quantity</b> <a>Int</a> </li> <li> <b>assetId</b> <a>ByteVector</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [LeaseTransaction](#LeaseTransaction) |   <ul> <li> <b>amount</b> <a>Int</a> </li> <li> <b>recipient</b><a>Address</a> <a>Alias</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [LeaseCancelTransaction](#LeaseCancelTransaction) |   <ul> <li> <b>leaseId</b> <a>ByteVector</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [MassTransferTransaction](#MassTransferTransaction) |   <ul> <li> <b>feeAssetId</b>  <a>OPTION(ByteVector)</a></li> <li> <b>assetId</b>  <a>OPTION(ByteVector)</a></li> <li> <b>totalAmount</b> <a>Int</a> </li> <li> <b>transfers</b> <a>LIST</a>[ [Transfer](#Transfer)]</li> <li> <b>transferCount</b> <a>Int</a> </li> <li> <b>attachment</b> <a>ByteVector</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [CreateAliasTransaction](#CreateAliasTransaction) |   <ul> <li> <b>alias</b> <a>String </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [SetScriptTransaction](#SetScriptTransaction) |   <ul> <li> <b>script</b>  <a>OPTION(ByteVector)</a></li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [SponsorFeeTransaction](#SponsorFeeTransaction) |   <ul> <li> <b>assetId</b> <a>ByteVector</a> </li> <li> <b>minSponsoredAssetFee</b>  <a>OPTION(Int)</a></li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [ExchangeTransaction](#ExchangeTransaction) |   <ul> <li> <b>buyOrder</b>[Order](#Order) </li> <li> <b>sellOrder</b>[Order](#Order) </li> <li> <b>price</b> <a>Int</a> </li> <li> <b>amount</b> <a>Int</a> </li> <li> <b>buyMatcherFee</b> <a>Int</a> </li> <li> <b>sellMatcherFee</b> <a>Int</a> </li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|
| [DataTransaction](#DataTransaction) |   <ul> <li> <b>data</b> <a>LIST</a>[ [DataEntry](#DataEntry)]</li> <li> <b>id</b> <a>ByteVector</a> </li> <li> <b>fee</b> <a>Int</a> </li> <li> <b>timestamp</b> <a>Int</a> </li> <li> <b>version</b> <a>Int</a> </li> <li> <b>sender</b><a>Address</a> </li> <li> <b>senderPublicKey</b> <a>ByteVector</a> </li> <li> <b>bodyBytes</b> <a>ByteVector</a> </li> <li> <b>proofs</b> <a>LIST</a> <a>ByteVector</a></li></ul>|

# Input variables
|vars|type|doc|
|-------|---|---|
| unit| [Unit](#Unit) | Single instance value|
| height| <a>Int</a> | Current blockchain height|
| tx| [Order](#Order) [TransferTransaction](#TransferTransaction) [IssueTransaction](#IssueTransaction) [ReissueTransaction](#ReissueTransaction) [BurnTransaction](#BurnTransaction) [LeaseTransaction](#LeaseTransaction) [LeaseCancelTransaction](#LeaseCancelTransaction) [MassTransferTransaction](#MassTransferTransaction) [CreateAliasTransaction](#CreateAliasTransaction) [SetScriptTransaction](#SetScriptTransaction) [SponsorFeeTransaction](#SponsorFeeTransaction) [ExchangeTransaction](#ExchangeTransaction) [DataTransaction](#DataTransaction)|  Processing transaction|


# Functions
|funcs|cost|doc|params|type|
|-------|-|---|---|---|
| fraction|1|Multiply and dividion with big integer intermediate representation|<ul> <li>value <a>Int</a> multiplyer</li> <li>numerator <a>Int</a> multiplyer</li> <li>denominator <a>Int</a> divisor</li></ul>| <a>Int</a>
| size|1|Size of bytes vector|<ul> <li>byteVector <a>ByteVector</a> vector</li></ul>| <a>Int</a>
| toBytes|1|Bytes array representation|<ul> <li>b  <a>Boolean</a> value</li></ul>| <a>ByteVector</a>
| toBytes|1|Bytes array representation|<ul> <li>n <a>Int</a> value</li></ul>| <a>ByteVector</a>
| toBytes|1|Bytes array representation|<ul> <li>s <a>String value</li></ul>| <a>ByteVector</a>
| take|1|Take firsts bytes subvector|<ul> <li>xs <a>ByteVector</a> vector</li> <li>number <a>Int</a> Bytes number</li></ul>| <a>ByteVector</a>
| drop|1|Skip firsts bytes|<ul> <li>xs <a>ByteVector</a> vector</li> <li>number <a>Int</a> Bytes number</li></ul>| <a>ByteVector</a>
| takeRight||Take vector tail|<ul> <li>@xs <a>ByteVector</a> vector</li> <li>@number <a>Int</a> taking size</li></ul>| <a>ByteVector</a>
| dropRight||Cut vectors tail|<ul> <li>@xs <a>ByteVector</a> vector</li> <li>@number <a>Int</a> cuting size</li></ul>| <a>ByteVector</a>
| size|1|Scting size in characters|<ul> <li>xs <a>String string</li></ul>| <a>Int</a>
| toString|1|String representation|<ul> <li>b  <a>Boolean</a> value</li></ul>| <a>String
| toString|1|String representation|<ul> <li>n <a>Int</a> value</li></ul>| <a>String
| take|1|Take string prefix|<ul> <li>xs <a>String sctring</li> <li>number <a>Int</a> prefix size in characters</li></ul>| <a>String
| drop|1|Remmove sring prefix|<ul> <li>xs <a>String string</li> <li>number <a>Int</a> prefix size</li></ul>| <a>String
| takeRight||Take string suffix|<ul> <li>@xs <a>String String</li> <li>@number <a>Int</a> suffix size in characters</li></ul>| <a>String
| dropRight||Remove string suffix|<ul> <li>@xs <a>String string</li> <li>@number <a>Int</a> suffix size in characters</li></ul>| <a>String
| _isInstanceOf|1|Internal function to check value type|<ul> <li>obj T value</li> <li>of <a>String type name</li></ul>|  <a>Boolean</a>
| isDefined||Check the value is defined|<ul> <li>@a OPTION[ T] Option value</li></ul>|  <a>Boolean</a>
| extract||Extract value from option or fail|<ul> <li>@a OPTION[ T] Optional value</li></ul>|  T
| throw|1|Fail script|<ul> <li>err <a>String Error message</li></ul>| [Nothing](#Nothing)
| throw||Fail script|<ul></ul>| [Nothing](#Nothing)
| *|1|Integer multiplication|<ul> <li>a <a>Int</a> multiplyer</li> <li>b <a>Int</a> multiplyer</li></ul>| <a>Int</a>
| /|1|Integer devision|<ul> <li>a <a>Int</a> divisible</li> <li>b <a>Int</a> divisor</li></ul>| <a>Int</a>
| %|1|Modulo|<ul> <li>a <a>Int</a> divisible</li> <li>b <a>Int</a> divisor</li></ul>| <a>Int</a>
| +|1|Integer sum|<ul> <li>a <a>Int</a> term</li> <li>b <a>Int</a> term</li></ul>| <a>Int</a>
| -|1|Integer substitution|<ul> <li>a <a>Int</a> term</li> <li>b <a>Int</a> term</li></ul>| <a>Int</a>
| +|10|Limited strings concatination|<ul> <li>a <a>String prefix</li> <li>b <a>String suffix</li></ul>| <a>String
| +|10|Limited bytes vectors concatination|<ul> <li>a <a>ByteVector</a> prefix</li> <li>b <a>ByteVector</a> suffix</li></ul>| <a>ByteVector</a>
| &#61;&#61;|1|Equality|<ul> <li>a T value</li> <li>b T value</li></ul>|  <a>Boolean</a>
| !&#61;||Inequality|<ul> <li>@a T value</li> <li>@b T value</li></ul>|  <a>Boolean</a>
| &gt;&#61;|1|Integer grater or equal comparation|<ul> <li>a <a>Int</a> term</li> <li>b <a>Int</a> term</li></ul>|  <a>Boolean</a>
| &gt;|1|Integer grater comparation|<ul> <li>a <a>Int</a> term</li> <li>b <a>Int</a> term</li></ul>|  <a>Boolean</a>
| getElement|2|Get list element by position|<ul> <li>arr LIST[ T] list</li> <li>pos <a>Int</a> element position</li></ul>|  T
| size|2|Size of list|<ul> <li>arr LIST[ T] list</li></ul>| <a>Int</a>
| -||Change integer sign|<ul> <li>@n <a>Int</a> value</li></ul>| <a>Int</a>
| !||unary negation|<ul> <li>@p  <a>Boolean</a> boolean</li></ul>|  <a>Boolean</a>
| keccak256|10|256 bit Keccak/SHA-3/TIPS-202|<ul> <li>bytes <a>ByteVector</a> value</li></ul>| <a>ByteVector</a>
| blake2b256|10|256 bit BLAKE|<ul> <li>bytes <a>ByteVector</a> value</li></ul>| <a>ByteVector</a>
| sha256|10|256 bit SHA-2|<ul> <li>bytes <a>ByteVector</a> value</li></ul>| <a>ByteVector</a>
| sigVerify|100|check signature|<ul> <li>message <a>ByteVector</a> value</li> <li>sig <a>ByteVector</a> signature</li> <li>pub <a>ByteVector</a> public key</li></ul>|  <a>Boolean</a>
| toBase58String|10|Base58 encode|<ul> <li>bytes <a>ByteVector</a> value</li></ul>| <a>String
| fromBase58String|10|Base58 decode|<ul> <li>str <a>String base58 encoded string</li></ul>| <a>ByteVector</a>
| toBase64String|10|Base64 encode|<ul> <li>bytes <a>ByteVector</a> value</li></ul>| <a>String
| fromBase64String|10|Base64 decode|<ul> <li>str <a>String base64 encoded string</li></ul>| <a>ByteVector</a>
| transactionById|100|Lookup transaction|<ul> <li>id <a>ByteVector</a> transaction Id</li></ul>| [Unit](#Unit) [GenesisTransaction](#GenesisTransaction) [PaymentTransaction](#PaymentTransaction) [TransferTransaction](#TransferTransaction) [IssueTransaction](#IssueTransaction) [ReissueTransaction](#ReissueTransaction) [BurnTransaction](#BurnTransaction) [LeaseTransaction](#LeaseTransaction) [LeaseCancelTransaction](#LeaseCancelTransaction) [MassTransferTransaction](#MassTransferTransaction) [CreateAliasTransaction](#CreateAliasTransaction) [SetScriptTransaction](#SetScriptTransaction) [SponsorFeeTransaction](#SponsorFeeTransaction) [ExchangeTransaction](#ExchangeTransaction) [DataTransaction](#DataTransaction)
| transactionHeightById|100|get height when transaction was stored to blockchain|<ul> <li>id <a>ByteVector</a> transaction Id</li></ul>| OPTION[ <a>Int</a>]
| getInteger|100|get data from the account state|<ul> <li>addressOrAlias <a>Address</a> <a>Alias</a> account</li> <li>key <a>String key</li></ul>| OPTION[ <a>Int</a>]
| getBoolean|100|get data from the account state|<ul> <li>addressOrAlias <a>Address</a> <a>Alias</a> account</li> <li>key <a>String key</li></ul>| OPTION[  <a>Boolean</a>]
| getBinary|100|get data from the account state|<ul> <li>addressOrAlias <a>Address</a> <a>Alias</a> account</li> <li>key <a>String key</li></ul>| OPTION <a>ByteVector</a>
| getString|100|get data from the account state|<ul> <li>addressOrAlias <a>Address</a> <a>Alias</a> account</li> <li>key <a>String key</li></ul>| OPTION[ <a>String]
| getInteger|10|Find and extract data by key|<ul> <li>data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>key <a>String key</li></ul>| OPTION[ <a>Int</a>]
| getBoolean|10|Find and extract data by key|<ul> <li>data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>key <a>String key</li></ul>| OPTION[  <a>Boolean</a>]
| getBinary|10|Find and extract data by key|<ul> <li>data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>key <a>String key</li></ul>| OPTION <a>ByteVector</a>
| getString|10|Find and extract data by key|<ul> <li>data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>key <a>String key</li></ul>| OPTION[ <a>String]
| getInteger||Extract data by index|<ul> <li>@data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>@index <a>Int</a> index</li></ul>| OPTION[ <a>Int</a>]
| getBoolean||Extract data by index|<ul> <li>@data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>@index <a>Int</a> index</li></ul>| OPTION[  <a>Boolean</a>]
| getBinary||Extract data by index|<ul> <li>@data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>@index <a>Int</a> index</li></ul>| OPTION <a>ByteVector</a>
| getString||Extract data by index|<ul> <li>@data LIST[ [DataEntry](#DataEntry)] DataEntry vector, usally tx.data</li> <li>@index <a>Int</a> index</li></ul>| OPTION[ <a>String]
| addressFromPublicKey||Convert public key to account address|<ul> <li>@publicKey <a>ByteVector</a> public key</li></ul>| <a>Address</a>
| addressFromString||Decode account address|<ul> <li>@string <a>String string address represntation</li></ul>| OPTION[ <a>Address</a>]
| addressFromRecipient|100|Extract address or lookup alias|<ul> <li>AddressOrAlias <a>Address</a> <a>Alias</a> address or alias, usually tx.recipient</li></ul>| <a>Address</a>
| assetBalance|100|get asset balance for account|<ul> <li>addressOrAlias <a>Address</a> <a>Alias</a> account</li> <li>assetId OPTION <a>ByteVector</a> assetId (WAVES if none)</li></ul>| <a>Int</a>
| wavesBalance||get WAVES balanse for account|<ul> <li>@addressOrAlias <a>Address</a> <a>Alias</a> account</li></ul>| <a>Int</a>


# Common fields
|tx type|id | fee| timestamp|version|sender|senderPublicKey|bodyBytes|proofs|
|---|---|---|---|---|---|---|---|---|
|TransferTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|IssueTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|ReissueTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|BurnTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|LeaseTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|LeaseCancelTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|MassTransferTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|CreateAliasTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|SetScriptTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|SponsorFeeTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|ExchangeTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|
|DataTransaction|  <a>ByteVector</a> |  <a>Int</a> |  <a>Int</a> |  <a>Int</a> |  <a>Address</a> |  <a>ByteVector</a> |  <a>ByteVector</a> |  LIST[<a>ByteVector</a>]|


 <h1>Transfers fields</h1><table><tr><td></td><td>PaymentTransaction</td><td>TransferTransaction</td><td>MassTransferTransaction</td><tr><tr><td>amount</td><td>  <a href="#Int">Int</a></td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>recipient</td><td>    <a href="#Address">Address</a> <a href="#Alias">Alias</a></td><td>    <a href="#Address">Address</a> <a href="#Alias">Alias</a></td><td>-</td></tr><tr><td>feeAssetId</td><td>-</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td></tr><tr><td>assetId</td><td>-</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td></tr><tr><td>attachment</td><td>-</td><td>  <a href="#ByteVector">ByteVector</a></td><td>  <a href="#ByteVector">ByteVector</a></td></tr><tr><td>totalAmount</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td></tr><tr><td>transfers</td><td>-</td><td>-</td><td>  LIST[<a href="#Transfer">Transfer</a>]</td></tr><tr><td>transferCount</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td></tr></table>

 <h1>Issuing assets fields</h1><table><tr><td></td><td>IssueTransaction</td><td>ReissueTransaction</td><td>BurnTransaction</td><td>SponsorFeeTransaction</td><tr><tr><td>quantity</td><td>  <a href="#Int">Int</a></td><td>  <a href="#Int">Int</a></td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>name</td><td>  <a href="#ByteVector">ByteVector</a></td><td>-</td><td>-</td><td>-</td></tr><tr><td>description</td><td>  <a href="#ByteVector">ByteVector</a></td><td>-</td><td>-</td><td>-</td></tr><tr><td>reissuable</td><td>  <a href="#Boolean">Boolean</a></td><td>  <a href="#Boolean">Boolean</a></td><td>-</td><td>-</td></tr><tr><td>decimals</td><td>  <a href="#Int">Int</a></td><td>-</td><td>-</td><td>-</td></tr><tr><td>script</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td><td>-</td><td>-</td><td>-</td></tr><tr><td>assetId</td><td>-</td><td>  <a href="#ByteVector">ByteVector</a></td><td>  <a href="#ByteVector">ByteVector</a></td><td>  <a href="#ByteVector">ByteVector</a></td></tr><tr><td>minSponsoredAssetFee</td><td>-</td><td>-</td><td>-</td><td>  OPTION[<a href="#Int">Int</a>]</td></tr></table>

 <h1>Leasing fields</h1><table><tr><td></td><td>LeaseTransaction</td><td>LeaseCancelTransaction</td><tr><tr><td>amount</td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>recipient</td><td>    <a href="#Address">Address</a> <a href="#Alias">Alias</a></td><td>-</td></tr><tr><td>leaseId</td><td>-</td><td>  <a href="#ByteVector">ByteVector</a></td></tr></table>

 <h1>Other fields</h1><table><tr><td></td><td>CreateAliasTransaction</td><td>SetScriptTransaction</td><td>ExchangeTransaction</td><td>DataTransaction</td><tr><tr><td>alias</td><td>  <a href="#String">String</a></td><td>-</td><td>-</td><td>-</td></tr><tr><td>script</td><td>-</td><td>  OPTION[<a href="#ByteVector">ByteVector</a>]</td><td>-</td><td>-</td></tr><tr><td>buyOrder</td><td>-</td><td>-</td><td>  <a href="#Order">Order</a></td><td>-</td></tr><tr><td>sellOrder</td><td>-</td><td>-</td><td>  <a href="#Order">Order</a></td><td>-</td></tr><tr><td>price</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>amount</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>buyMatcherFee</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>sellMatcherFee</td><td>-</td><td>-</td><td>  <a href="#Int">Int</a></td><td>-</td></tr><tr><td>data</td><td>-</td><td>-</td><td>-</td><td>  LIST[<a href="#DataEntry">DataEntry</a>]</td></tr></table>
