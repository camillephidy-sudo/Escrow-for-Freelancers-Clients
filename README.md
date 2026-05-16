# Merkle Tree Gift List

A demonstration of using Merkle Trees for efficient membership verification in a blockchain-inspired context. This project implements a "gift list" where the server only stores a single 32-byte Merkle root, yet can verify if a client is on the list without storing the entire list.

## Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API](#api)
- [Adding Your Name](#adding-your-name)
- [Contributing](#contributing)

## Overview

This project addresses a key blockchain storage problem: nodes must store all data, but storage is expensive. By using Merkle Trees, we can prove membership in a large dataset with minimal data storage.

- **Client (Prover)**: Generates a Merkle proof for their name and sends it to the server.
- **Server (Verifier)**: Verifies the proof against the stored Merkle root.

## How It Works

Merkle Trees allow efficient verification of data integrity and membership. Here's the flow:

1. A Merkle Tree is built from the list of names.
2. The root hash is stored on the server.
3. To prove a name is on the list, the client provides:
   - The name
   - A proof (list of hashes from the leaf to the root)
4. The server verifies the proof by reconstructing the path to the root.

This ensures the server only needs 32 bytes (the root) to verify any name from a potentially massive list.

## Installation

1. Install dependencies:
   ```bash
   npm install
   ```

## Usage

### Running the Example

1. Start the server:
   ```bash
   node server/index.js
   ```

2. In another terminal, run the client:
   ```bash
   node client/index.js
   ```

The client will send a proof for "GitHub Copilot" and receive a gift if verified.

### Testing the Merkle Tree

Run the example script:
```bash
node utils/example.js
```

This verifies that "Norman Block" is in the tree.

## Project Structure

```
.
├── client/
│   └── index.js          # Client script that generates and sends proofs
├── server/
│   └── index.js          # Express server that verifies proofs
├── utils/
│   ├── MerkleTree.js     # Merkle Tree implementation
│   ├── verifyProof.js    # Proof verification function
│   ├── niceList.json     # List of names on the gift list
│   └── example.js        # Example usage
├── package.json          # Dependencies
└── README.md             # This file
```

## API

### POST /gift

Verifies if a name is on the gift list.

**Request Body:**
```json
{
  "name": "string",
  "proof": [
    {
      "data": "hex_string",
      "left": boolean
    }
  ]
}
```

**Response:**
- Success: `"You got a toy robot!"`
- Failure: `"You are not on the list :("`

## Adding Your Name

To add your name to the gift list:

1. Edit `utils/niceList.json` and add your name to the array.

2. Recompute the Merkle root:
   ```bash
   node -e "const MerkleTree = require('./utils/MerkleTree'); const niceList = require('./utils/niceList.json'); const tree = new MerkleTree(niceList); console.log(tree.getRoot());"
   ```

3. Update the `MERKLE_ROOT` in `server/index.js` with the new hash.

4. Modify `client/index.js` to use your name.

## Contributing

Feel free to improve the implementation, add tests, or enhance the documentation. This is an educational project for learning about Merkle Trees in blockchain contexts.
