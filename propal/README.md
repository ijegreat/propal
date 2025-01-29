# Propal Smart Contract

A decentralized blockchain-based property registry system that enables secure ownership tracking and transfer of real estate assets through smart contracts.

## Overview

Propal is a non-fungible token (NFT) based property management system that allows for:
- Registration of property assets with detailed information
- Secure transfer of property ownership
- Property valuation updates
- Geographic and zoning information management
- Cryptocurrency-based property purchases

## Features

### Property Registration
- Create new property entries with:
  - Detailed property information
  - Current valuation
  - Geographic data
  - Zoning information
- Each property is minted as a unique NFT
- Automatic property ID generation

### Ownership Management
- Secure transfer of property ownership using digital signatures
- Ownership verification system
- Integration with cryptocurrency for property purchases

### Property Information Management
- Update property valuations
- Modify geographic data
- Update zoning information
- Retrieve property details

## Functions

### Public Functions

`register-property`
- Registers a new property in the system
- Parameters: property-info, valuation, geographic-data, zoning-info
- Returns: property ID

`transfer-property`
- Transfers property ownership to a new owner
- Parameters: property-id, new-owner, digital-signature
- Requires signature validation

`update-property-valuation`
- Updates the valuation of an existing property
- Parameters: property-id, new-valuation
- Only callable by current owner

`update-geographic-data`
- Updates the geographic data of a property
- Parameters: property-id, new-geographic-data
- Only callable by current owner

`update-zoning-info`
- Updates zoning information
- Parameters: property-id, new-zoning-info
- Only callable by current owner

`purchase-property`
- Facilitates property purchase using cryptocurrency
- Parameters: property-id, crypto-tx-hash
- Verifies payment before transfer

### Read-Only Functions

`get-property-details`
- Retrieves all details of a property
- Parameters: property-id

`verify-ownership`
- Verifies if a given principal owns a specific property
- Parameters: property-id, owner

## Error Codes

- `u400`: Invalid valuation (must be greater than zero)
- `u401`: Invalid property information or signature validation failed
- `u402`: Invalid signature or cryptocurrency payment
- `u403`: Unauthorized access (not the current owner)
- `u404`: Property not found
- `u405`: Invalid transfer (new owner same as current owner)
- `u406`: Invalid digital signature
- `u407`: Invalid geographic data
- `u408`: Invalid zoning information

## Security Features

- Digital signature validation for ownership transfers
- Cryptocurrency payment verification
- Owner-only access control for updates
- Non-fungible token (NFT) based ownership tracking

## Dependencies

- Requires a blockchain environment supporting:
  - NFT functionality
  - Digital signature validation
  - Smart contract execution
  - Cryptocurrency transactions

## Future Improvements

- Implementation of proper cryptocurrency payment validation
- Addition of property history tracking
- Support for multiple ownership structures
- Integration with real-world property databases
- Enhanced validation for geographic and zoning data
- Support for property documentation storage