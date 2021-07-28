# GraphQL Schema Basics

## Basics <a id="basics"></a>

The core idea of the GraphQL API is to describe available entities and attributes with a schema and let client decide which parts, elements and services it needs to perform its operation. Our schema is extensively commented and you should be able to grab the right data just by comparing your needs with the schema. Please let us know if you would still miss anything important.

The API server supports introspection. It means that with a competent development tool you can scan the available structure and build your GraphQL queries with full support of known structure.

## Conventions <a id="conventions"></a>

The API follows this conventions and recommendations:

* GraphQL types are Capital Camel Case.
* Attributes are regular camel Case.
* Function calls are named and managed the same way as attributes.
* Complex input and output values are encapsulated in a type instead of expanded list.
* Each type, attribute and function has a comment describing it's purpose.

## Scalar Values <a id="scalar-values"></a>

The API uses several different scalar values besides the default GraphQL set. Most of them encode big values, or byte arrays of hashes and addresses. If your client application is build using JavaScript, or TypeScript, you can benefit from using excellent [Ethereum Web3.js](https://github.com/ethereum/web3.js/) library, which can help you deal with decoding and validating process of most data types used here.

Transaction amounts, account balances, rewards and basically all amount related data are transferred as big integers encoded in prefixed hexadecimal format. It represents the smallest indivisible amount of value inside the block chain, so called WEI.

One FTM token contains 10¹⁸ WEIs.

Following scalar values are used by the API:

* **Hash** is a 32 byte binary string, represented by 0x prefixed hexadecimal number.
* **Address** is a 20 byte Opera address, represented by 0x prefixed hexadecimal number.
* **BigInt** is a large integer value. Input is accepted as either a JSON number, or a hexadecimal number alternatively prefixed with 0x. Output is 0x prefixed hexadecimal.
* **Long** is a 64 bit unsigned integer value represented by 0x prefixed hexadecimal number.
* **Bytes** is an arbitrary length binary string, represented by 0x-prefixed hexadecimal string. An empty byte string is represented by '0x'.
* **Cursor** is an unspecified string value representing position in a sequential list of edges. Please see following section for details about Cursor usage.

The API uses cursor based pagination. We didn't use well known and extensively used, or very similar architecture, where you deal with numeric offset of a collection member from the top of the collection. In our use case the collection top can be changing constantly and keeping track of your position in the collection with ever changing anchor is nearly impossible.

The solution we use is based on a **cursor**. Each member of the collection has a unique identifier called **cursor.** When you want to obtain a slice of the collection, you simply specify the **cursor** value of the collection member and a count of how many neighbors of that anchor you need.

If you do not specify the **cursor**, we assume you mean either top, or bottom of the collection. The relative anchor is determined by the value of your neighbors count.

For example this query provides 15 consecutive block after the one with **cursor** "0x134b7".

```text
query BlocksList {    blocks (cursor: "0x134b7", count: 15) {        totalCount        pageInfo {            first            last            hasNext            hasPrevious        }        edges {            cursor            block {                hash                number                timestamp                transactionCount            }        }    }}
```

If you just want 10 most recent transaction, you will skip the cursor and send the following query:

```text
query TransactionsList {    transactions (count: 10) {        totalCount        pageInfo {            first            last            hasNext            hasPrevious        }        edges {            cursor            transaction {                hash                from                to                value                block {                    timestamp                }            }        }    }}
```

Please note that each response will contain several important information which will help you navigate through the collection.

First is the **pageInfo** structure, defined by **PageInfo** type. It contains the first and last **cursor** of your current slice so you can use these values and ask for next **X** edges, or previous **-X** edges.

Also each **edge** of the list contains not only the desired data element, but also a **cursor**, which can be used to create a link, if desired, to the same position in the collection regardless of the absolute distance of the element from the top, or bottom.

