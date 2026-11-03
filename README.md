# FlapJax Treasury Outflow Audit — 2026-11-01 (COT, UTC-5)

Independent on-chain audit prepared for FlapJax paid task Q86 (TaskMarket TSK-Y8ZWGHP4).
Auditor handle: **Sisca876** (GitHub). All data below comes from the BSC chain alone
(public archive RPC: `eth_getLogs`, `eth_getBalance`, `eth_getTransactionCount`, full-block reads).

## Scope

- Token: FLAPJAX `0x90c8889f428F9Ebb77BB8f15CAD3a50a9aC680df` (18 decimals)
- Treasury: `0x7C34E9e21eE28A49Ff0b84B61774119E6633359f`
- Window: 2026-11-01 00:00:00 to 23:59:59 COT (UTC-5) = 05:00 UTC Nov 1 to 05:00 UTC Nov 2
- Block range scanned: 130989236–131181186 (every `Transfer` log with `from` = treasury)

## Headline numbers

- **Transfers out: 20**
- **Total sent: 7275000 FLAPJAX**
- **Distinct recipients: 17**
- **Distinct operators implied by first-funder groups: 16** (see grouping below).
  14 of 17 recipients were **never funded with BNB at all** (nonce 0, zero balance at payout
  and at audit time), so no on-chain funder link exists for them; only 3 recipients have a
  traceable first funder, and 2 of those 3 were funded by the treasury itself.

## Every transfer (times in COT)

| # | Tx hash | Block | Time (COT) | Recipient | Amount (FLAPJAX) |
|---|---------|-------|------------|-----------|------------------|
| 1 | 0x359f40e334ebc0cf3477cf465bb215c12d68e233829abbcc622ce200fed0a16c | 131058409 | 2026-11-01 08:38:58 | 0xdf4ff9d2f45f99f11a90b16f277d4b7edddb72a5 | 25000 |
| 2 | 0xe33c65122ca18b07afa19bc2175ee9c756f11517bf719bc41e472c5167673801 | 131058441 | 2026-11-01 08:39:12 | 0xabc2c3daffa4c1963299da225c25f2aa7d4ddf62 | 25000 |
| 3 | 0x67caa95b779edd611a3d6fc2168e94c5380a0413916295e36e22d1d8c3120b79 | 131058476 | 2026-11-01 08:39:28 | 0xfb200657f7266157a45dfcc6c09690726daa24e6 | 25000 |
| 4 | 0x2193304d6a26d776a2cef575f0b743f810ef9a4de7aa4ad40fef3af3ef4629d1 | 131058510 | 2026-11-01 08:39:43 | 0xeba13671a2f1993ee26a4e286db6e491fa5c99bc | 25000 |
| 5 | 0x81c497dc743236d0d9fdcc9c121b178cb8814d66a48593f973ac6a84c0841f0c | 131058547 | 2026-11-01 08:40:00 | 0xca58696564492ef9c3229c89072365b253bda246 | 100000 |
| 6 | 0x14380a49d87c6b475b3ff959e804189aa8205b6fad3e4a99c5293d9015991c90 | 131058588 | 2026-11-01 08:40:18 | 0xa15c58e7008fc7a0331cfcc86a28af99fd21b93c | 100000 |
| 7 | 0x603db27dd58cbd1561b6c8af41552cdf6e1cdcc100ffe0bc730c6d2e03e8b90c | 131073418 | 2026-11-01 10:31:34 | 0xa15c58e7008fc7a0331cfcc86a28af99fd21b93c | 25000 |
| 8 | 0xe92e94144472a1b7c6cedefd2f64d6c549037196b65c65399e72d7f02e72156e | 131080128 | 2026-11-01 11:21:54 | 0xfdf05af8ddce3621f01713e01721d6e9ad702ea8 | 25000 |
| 9 | 0xab410d4b5c60288fa44aa09a5119ee42650785eaf9ae1aa42ab4c0874335342a | 131088758 | 2026-11-01 12:26:39 | 0xec2f03b4baa1dc49559e56a54f84a2e9f2a30a91 | 25000 |
| 10 | 0x86cd9655cead2eb372ec3874c0a136b2d38110bd7ab25f32f15bce6ca42650b4 | 131120212 | 2026-11-01 16:22:36 | 0xe8797a6bb4693674d78e933e85cb159a0219d03b | 25000 |
| 11 | 0x96100d7abf13ab50a08b0baac1e94de20d8c725d8fc2e9b9692a62e42b3fffa3 | 131145205 | 2026-11-01 19:30:04 | 0x16fed0d8d3777a002b569c649ffff37d6d9303c9 | 250000 |
| 12 | 0x4bab3fe13c1e9904b68d574659eac8423fe564c09dbb1bfcf51bfbedbd65c19f | 131145277 | 2026-11-01 19:30:37 | 0x4a4b89974b5cda4cbd9cd9bc84b5d2dbfd7018e6 | 250000 |
| 13 | 0x45b002a93bc098497d466f258ef9ecd1c2216a851ce7a5b2abee4a1137a6cb09 | 131145340 | 2026-11-01 19:31:05 | 0xf325475201477745f3956f815edb50e8c16426ba | 250000 |
| 14 | 0x805bc502e5c1145f57e798433b4cf5caa915d872ec9164b7ff35b22db50deae6 | 131145404 | 2026-11-01 19:31:34 | 0x655186eb71353ba93063742fb42c2bae59af196e | 250000 |
| 15 | 0x784c7d55f318c6a3a918549fbfe49e4786af4da4bbb3a7a51f042a6d23c25808 | 131145806 | 2026-11-01 19:34:35 | 0x97cd18b8bbb629b17675d868259ea84c0a2a5a9c | 3000000 |
| 16 | 0xd99981608b6990fe206b111290e2a77b84140132cd8f91e351cf4e94d47ca947 | 131145869 | 2026-11-01 19:35:03 | 0x4644f7b8679bf0b6f22e69408e2272e9f4417b45 | 250000 |
| 17 | 0xa8ef0a78354b5ece0cf5dfcce06ad3879bfb6fc3bee82210d664715ed357c193 | 131145936 | 2026-11-01 19:35:33 | 0xca58696564492ef9c3229c89072365b253bda246 | 300000 |
| 18 | 0x056cf562378d5d859f422e4d2d92667570a37ac261b504f0c2c9efa935cf8f74 | 131146078 | 2026-11-01 19:36:37 | 0xeba13671a2f1993ee26a4e286db6e491fa5c99bc | 300000 |
| 19 | 0xd9ab8bc50bed3bfa44a4e754407dec81e4fe7f2ac32c366009e3bcfb4e1702d1 | 131168762 | 2026-11-01 22:26:47 | 0xb1051c2b38ad3efefc7ff5fb61d7068bd031b81e | 25000 |
| 20 | 0x69e239a56715d6ae0dac697b88877a0a9514f64a0ccd8ee95bb8bce91c9b8c0e | 131175568 | 2026-11-01 23:17:50 | 0x3aeae5f742e34f94db19b6c494072957633fa7ca | 2000000 |

## Recipients and first BNB funder

| Recipient | Total received | Payouts | First BNB funder | Evidence |
|-----------|---------------|---------|------------------|----------|
| 0xdf4ff9d2f45f99f11a90b16f277d4b7edddb72a5 | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xabc2c3daffa4c1963299da225c25f2aa7d4ddf62 | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xfb200657f7266157a45dfcc6c09690726daa24e6 | 25000 | 1 | 0x7c34e9e21ee28a49ff0b84b61774119e6633359f | funding tx 0xa3d7042983f4f2352b9b8f324414688db10887e2b2b2a125deca9a8bec6624e7 (block 126835408, 0.0005 BNB) |
| 0xeba13671a2f1993ee26a4e286db6e491fa5c99bc | 325000 | 2 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xca58696564492ef9c3229c89072365b253bda246 | 400000 | 2 | 0x7c34e9e21ee28a49ff0b84b61774119e6633359f | funding tx 0x87443eff758296585f6d6eb7b68800ea6c73f143239e60541a6ef5b1f072d456 (block 130097514, 0.0005 BNB) |
| 0xa15c58e7008fc7a0331cfcc86a28af99fd21b93c | 125000 | 2 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xfdf05af8ddce3621f01713e01721d6e9ad702ea8 | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xec2f03b4baa1dc49559e56a54f84a2e9f2a30a91 | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xe8797a6bb4693674d78e933e85cb159a0219d03b | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0x16fed0d8d3777a002b569c649ffff37d6d9303c9 | 250000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0x4a4b89974b5cda4cbd9cd9bc84b5d2dbfd7018e6 | 250000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xf325475201477745f3956f815edb50e8c16426ba | 250000 | 1 | 0x3ce2c77570a651bd344beb3d3d610aa0548c8ac8 | funding tx 0xb97bc7b736553fcb93c8e65dea438acc126bdfd4abad9963559ef17391348792 (block 130818784, 0.0002 BNB) |
| 0x655186eb71353ba93063742fb42c2bae59af196e | 250000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0x97cd18b8bbb629b17675d868259ea84c0a2a5a9c | 3000000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0x4644f7b8679bf0b6f22e69408e2272e9f4417b45 | 250000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0xb1051c2b38ad3efefc7ff5fb61d7068bd031b81e | 25000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |
| 0x3aeae5f742e34f94db19b6c494072957633fa7ca | 2000000 | 1 | — none — | virgin EOA: nonce 0, no contract code, zero BNB balance at payout and at audit time — never funded |

## Funder groups (operator clusters)

- **Group T — first funder = the treasury itself** (`0x7c34e9e21ee28a49ff0b84b61774119e6633359f`):
  `0xfb200657f7266157a45dfcc6c09690726daa24e6` (25,000) and `0xca58696564492ef9c3229c89072365b253bda246` (400,000).
  Per the task rule these group **with the treasury**.
- **Group X — first funder `0x3ce2c77570a651bd344beb3d3d610aa0548c8ac8`**:
  `0xf325475201477745f3956f815edb50e8c16426ba` (250,000). Singleton group.
- **14 unfunded singletons**: the remaining 14 recipients share no first funder (they have none).
  Counting each as its own cluster: 14 + Group T + Group X = **16 distinct operator clusters**
  as a *lower bound on distinct funders*, with the caveat that unfunded wallets cannot be
  attributed to any operator from chain data alone — one operator could control many of them.

## Patterns and items that could not be explained

- Nine payouts of exactly 25,000 and five of exactly 250,000 look like standard task/reward
  tranches. Three recipients were paid twice: `0xca586965…` (100,000 + 300,000),
  `0xeba13671…` (25,000 + 300,000) and `0xa15c58e7…` (100,000 + 25,000).
- **Unexplained concentration:** the two largest transfers — **3,000,000** to `0x97cd18b8…` and
  **2,000,000** to `0x3aeae5f7…` — together 5,000,000 of the day's 7,275,000 (68.7%) went to
  wallets that were never funded with BNB and have never made a transaction. Nothing on-chain
  in the window explains what these two payouts were for; they do not resemble the 25,000 /
  250,000 reward tranches.
- All 14 unfunded recipients are **unexplained as 'separate operators'**: with no BNB funding
  event and nonce 0, chain data offers no evidence that they are distinct people rather than
  freshly generated addresses from one operator. Recipients who *were* funded by the treasury
  itself (Group T) are, by the task's own grouping rule, linked to the treasury.
- Payout transactions are plain ERC-20 `transfer` calls sent by the treasury EOA directly to
  the token contract (verified on tx `0x359f40e3…`: from = treasury, to = token, value 0).

## Method (reproducible)

1. Located the COT window's block range by binary search on block timestamps.
2. `eth_getLogs` for FLAPJAX `Transfer` events with `from` = treasury in 5,000-block chunks
   over the full range (0 failed chunks; 20 logs). Times converted UTC → COT (−5h).
3. First-funder trace per recipient: binary search on historical `eth_getBalance` (archive
   node) for the first block with a positive balance, then confirmed the funding transaction
   inside that block. Cross-checked with `eth_getCode` and `eth_getTransactionCount`.
4. Negative results are stated as found: a recipient with zero balance at the payout block
   *and* at the latest block, nonce 0 and no code, has no on-chain BNB funder.

Raw transfer data: see `transfers.csv` in this repository.
