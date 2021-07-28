# Issue TRC-10 token

wallet/createassetissue

Description: Issue a token

demo: curl -X POST http://127.0.0.1:8090/wallet/createassetissue -d '{

"owner\_address":"41e552f6487585c2b58bc2c9bb4492bc1f17132cd0",

"name":"0x6173736574497373756531353330383934333132313538",

"abbr": "0x6162627231353330383934333132313538",

"total\_supply" :4321,

"trx\_num":1,

"num":1,

"start\_time" : 1530894315158,

"end\_time":1533894312158,

"description":"007570646174654e616d6531353330363038383733343633",

"url":"007570646174654e616d6531353330363038383733343633",

"free\_asset\_net\_limit":10000,

"public\_free\_asset\_net\_limit":10000,

"frozen\_supply":{"frozen\_amount":1, "frozen\_days":2}

}'

Parameter owner\_address: Owner address, default hexString

Parameter name: Token name, default hexString

Parameter abbr: Token name abbreviation, default hexString

Parameter total\_supply: Token total supply

Parameter trx\_num: Define the price by the ratio of trx\_num/num,

Parameter num: Define the price by the ratio of trx\_num/num

Parameter start\_time: ICO start time

Parameter end\_time: ICO end time

Parameter description: Token description, default hexString

Parameter url: Token official website url, default hexString

Parameter free\_asset\_net\_limit: Token free asset net limit

Parameter public\_free\_asset\_net\_limit: Token public free asset net limit

Parameter frozen\_supply: Token frozen supply

Parameter permission\_id: Optional, for multi-signature use

Return: Transaction object

Note: The unit of 'trx\_num' is SUN

