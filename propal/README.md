# Propal Smart Contract

## Overview
The Propal Smart Contract is a decentralized proof-of-ownership system implemented in Clarity for managing real estate property records on the blockchain. It enables property registration, ownership transfers, and property information management in a secure and transparent manner.

## Features
- Property registration with detailed information
- Secure ownership transfers with digital signatures
- Property valuation management
- Geographic and zoning information updates
- Cryptocurrency-based property purchases
- Ownership verification system

## Contract Functions

### Core Property Management

#### `register-property`
Registers a new property in the system.
```clarity
(register-property 
  property-info: (string-ascii 256)
  valuation: uint
  geographic-data: (string-ascii 256)
  zoning-info: (string-ascii 100)
) -> (response uint uint)
```
- Returns: Property ID on success, error code on failure

#### `transfer-property`
Transfers property ownership to a new owner.
```clarity
(transfer-property 
  property-id: uint
  new-owner: principal
  digital-signature: (buff 65)
) -> (response bool uint)
```
- Requires digital signature verification
- Returns: Success/failure status

#### `verify-ownership`
Verifies if a specific principal owns a property.
```clarity
(verify-ownership 
  property-id: uint
  owner: principal
) -> (response bool uint)
```
- Returns: True if owner matches, false otherwise

### Property Information Management

#### `update-property-valuation`
Updates the property's valuation.
```clarity
(update-property-valuation 
  property-id: uint
  new-valuation: uint
) -> (response bool uint)
```

#### `update-geographic-data`
Updates property's geographic information.
```clarity
(update-geographic-data 
  property-id: uint
  new-geographic-data: (string-ascii 256)
) -> (response bool uint)
```

#### `update-zoning-info`
Updates property's zoning information.
```clarity
(update-zoning-info 
  property-id: uint
  new-zoning-info: (string-ascii 100)
) -> (response bool uint)
```

#### `get-property-details`
Retrieves all details about a specific property.
```clarity
(get-property-details 
  property-id: uint
) -> (optional {property-data})
```

### Property Purchase

#### `purchase-property`
Facilitates property purchase using cryptocurrency.
```clarity
(purchase-property 
  property-id: uint
  crypto-tx-hash: (buff 32)
) -> (response bool uint)
```

## Error Codes
- `u400`: Invalid valuation (must be greater than 0)
- `u401`: Invalid property information or signature validation failure
- `u402`: Invalid cryptocurrency payment or signature recovery error
- `u403`: Unauthorized action (not the current owner)
- `u404`: Property not found
- `u405`: Invalid new owner (same as current owner)
- `u406`: Invalid digital signature (empty)
- `u407`: Invalid geographic data (empty)
- `u408`: Invalid zoning information (empty)

## Data Structures

### Property Registry Entry
```clarity
{
  current-owner: principal,
  property-info: (string-ascii 256),
  valuation: uint,
  geographic-data: (string-ascii 256),
  zoning-info: (string-ascii 100)
}
```

## Security Features
- Digital signature verification for property transfers
- Owner-only access for property updates
- Cryptocurrency payment validation
- Non-fungible token (NFT) based ownership representation

## Usage Examples

### Registering a New Property
```clarity
(register-property 
  "123 Main St, Floor 3, Unit 301" 
  u500000 
  "40.7128°N, 74.0060°W" 
  "R-1: Residential"
)
```

### Transferring Property
```clarity
(transfer-property 
  u1 
  'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7 
  0x123...
)
```

### Verifying Property Ownership
```clarity
(verify-ownership 
  u1 
  'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7
)
```

## Best Practices
1. Always verify property ownership before initiating transfers
2. Keep accurate and up-to-date property information
3. Maintain secure digital signatures for all transfers
4. Validate cryptocurrency transactions thoroughly
5. Regular updates of property valuations and information
