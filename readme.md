# QRTs

QRTs are ERC721 artworks, that can be scanned to parse a 40-character hexadecimal seed phrase. That seed phrase allows looking up records set by the owner in the QRT registry, located at qrt.eth.

---

## Contracts

This strategy is based loosely on that used by Decentraland to encapsulate their Avatars as ERC721.

- **QRTRegistrar** - ERC721, ownership records (https://github.com/decentraland/avatars-contract/blob/master/contracts/ens/DCLRegistrar.sol)
- **QRTController** - owns QRTRegistrar, used by app to register Glyphs (https://github.com/decentraland/avatars-contract/blob/master/contracts/ens/DCLController.sol)
- **PriceOracle** (allows stable pricing of QRTs while still accepting payments in ETH) (https://github.com/ensdomains/ethregistrar/blob/master/contracts/LinearPremiumPriceOracle.sol)
- **QRTReverseRegistrar** - manages reverse lookups (https://github.com/ensdomains/ens/blob/master/contracts/ReverseRegistrar.sol)

---

## Deployments
1. Deploy **QRTRegistrar**(*ensRegistry, ensRegistrarBase, “eth”, “qrt”, baseUri*)
2. Deploy **PriceOracle**()
3. Deploy **QRTController**(*QRTRegistrar, priceOracle*)
4. Call `setController(QRTController)` on QRTRegistrar

---

## Phases
### Announcement
- Publicly announce project and reveal art

### Deploy
- Contracts are deployed

### Phase 1 (48 hours)
- Glyphs can only be minted by owners of Tiles with matching seed address
- Transfers not allowed
- 50% discount

### Phase 2 (48 hours)
- Glyphs can only be minted by owners of at least 1 Tile NFT
- Transfers not allowed
- 50% discount

### Final phase
- Glyphs are mintable and transferable by all

---

## Mechanics
- own qrt.eth
- User mints qrt for a specific seed address
	- <seed>.qrt.eth is registered on ENS registry
- Owner of qrt can update all ENS records of <seed.qrt.eth> through QRTController (`registry.setSubnodeRecord()`)
- Registered qrts do not expire
- Users can set reverse record for any qrt they own. Points ETH wallet -> qrt

---

## Pricing
The below pricing tiers are designed so that "orderly" QRTs more expensive. 

*X* = some price. If we use a price oracle, *X* could be something stable (e.g. 5,000 DAI), but we can also just make it 1 ETH.

- **If all characters in seed are the same:** 1*X* (only 16 of these)
- **If more than 50% characters in seed are the same:** 0.1*X*
- **If more than 25% characters in seed are the same:** 0.01*X*
- **All others:** 0.001*X*

---

## App
- Shop for and mint unminted glyphs
- Browse minted glyphs