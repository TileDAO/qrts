ETGs launch

## Contracts
**GlyphRegistrar** - ERC721, ownership records
**GlyphController** - owns GlyphRegistrar, used by app to register Glyphs
**PriceOracle** (maybe)
**GlyphReverseRegistrar**


## Deployments
	1. Deploy **GlyphRegistrar**(*ensRegistry, ensRegistrarBase, “eth”, “qrt”, baseUri*)
	2. Deploy **PriceOracle**()
	3. Deploy **GlyphController**(*glyphRegistrar, priceOracle*)
	4. Call `setController(GlyphController)` on GlyphRegistrar


## Phases
### Announcement
	- Publicly announce project and reveal art

### Deploy
	* Contracts are deployed

### Phase 1 - 48 hours
	- Glyphs can only be minted by owners of Tiles with matching seed address
	- Transfers not allowed
	- 50% discount

### Phase 2 - 48 hours
	* Glyphs can only be minted by owners of at least 1 Tile NFT
	* Transfers not allowed
	* 50% discount

### Final phase
	* Glyphs are mintable and transferable by all


## Mechanics
	* own qrt.eth
	* User mints glyph for a specific seed address
		* <seed>.qrt.eth is registered on ENS registry
	* Owner of glyph can update all ENS records of <seed.qrt.eth> through GlyphController (`registry.setSubnodeRecord()`)
	* Registered glyphs do not expire
	* Users can set reverse record for any glyph they own. Points ETH wallet -> glyph


## Pricing
X denotes some price. If we use a price oracle, X could be something more stable like 5000 DAI, but we can also just make it 1 ETH.
	- **If all characters in seed are the same:** 1x (only 16 of these)
	- **If more than 50% characters in seed are the same:** 0.1x
	- **If more than 25% characters in seed are the same:** 0.01x
	- **Else:** 0.001x


## App
	* Shop for and mint unminted glyphs
	* Browse minted glyphs