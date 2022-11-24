# stacks-node-cli

Stacks node swiss-army knife

## Encoding Clarity values

```
$ ./stacks-node-cli encode
Usage: ./stacks-node-cli encode type value [type value ...]
Where `type` and `value` adhere to the following grammar:
(note that '++' means 'concatenation')

   Integer         = (any i128 value)
   UInteger        = (any u128 value)
   C32Address      = (any Crockford-32 checksum-encoded address)
   HexString       = "0x" ++ (any string that matches the regex /^[0-9a-f]$/)
   ClarityLiteral  = (any string that is a valid Clarity literal)
   ContractName    = (any string that is a valid Clarity contract name)
   ASCIIString     = " ++ (any string made of just ASCII characters) ++ "
   UTF8String      = " ++ (any string made of UTF-8 codepoints) ++ "

   AddressString   = C32Address | C32Address, ContractName

   Value = Integer | UInteger | C32CheckString | Boolean | HexString | ASCIIString | UTF8String 

   Type = "int", Integer | "uint", UInteger | "bool", Boolean | "buff", HexString |
          "string-ascii", ASCIIString | "string-utf8", UTF8String | "principal", AddressString |
          "some", Type | "none" | "ok", Type | "err", Type | "list", UInteger, { Type, Value } |
          "tuple", UInteger, { ClarityLiteral, Type, Value }

Examples:
 uint 3
       0100000000000000000000000000000003
 principal SP1QK1AZ24R132C0D84EEQ8Y2JDHARDR58R72E1ZW
       05166f30abe2260231300d411ceba3c29362ac370546
 buff 0x1234
       02000000021234
 some buff 0xdeadbeef
       0a0200000004deadbeef
 ok some string-ascii "hello world"
       070a0d0000000b68656c6c6f20776f726c64
 list 3 uint 0 uint 1 uint 2
       0b00000003010000000000000000000000000000000001000000000000000000000000000000010100000000000000000000000000000002
 tuple 2 field1 int 3 field2 string-utf8 "hello world"
       0c00000002066669656c64310000000000000000000000000000000003066669656c64320e0000000b68656c6c6f20776f726c64
```

TODO: finish the rest of the README
