# FlexLease: Decentralized Equipment/Vehicle Rental Protocol
## Technical Specification Document v1.0

---

## 1. Project Overview and Objectives

### 1.1 Project Name
**FlexLease** - A decentralized peer-to-peer equipment and vehicle rental protocol built on the Stacks blockchain.

### 1.2 Vision Statement
FlexLease aims to democratize access to expensive equipment and vehicles by enabling fractional ownership, transparent rental agreements, and trustless peer-to-peer transactions. By leveraging blockchain technology, we eliminate intermediaries, reduce costs, and create new revenue opportunities for asset owners.

### 1.3 Core Problem Statement
- High capital requirements prevent individuals and small businesses from accessing expensive equipment
- Traditional rental platforms charge high intermediary fees (20-40%)
- Lack of transparency in ownership verification and maintenance history
- Limited liquidity for equipment owners who want to monetize idle assets
- Trust issues in peer-to-peer rentals without proper escrow mechanisms
- Difficulty in establishing fractional ownership of high-value assets

### 1.4 Solution Overview
FlexLease provides a decentralized protocol that:
- Tokenizes physical assets into verifiable on-chain representations
- Enables fractional ownership through token splits
- Facilitates trustless rentals via smart contract escrow
- Distributes rental revenue automatically to token holders
- Builds transparent reputation systems for both owners and renters
- Integrates decentralized insurance mechanisms

### 1.5 Primary Objectives
1. Create a seamless asset tokenization process for equipment owners
2. Build a secure P2P rental marketplace with automated escrow
3. Enable fractional ownership to lower entry barriers
4. Implement fair revenue distribution based on ownership stakes
5. Establish reputation and insurance systems to minimize risk
6. Achieve <5% platform fee (compared to 20-40% in traditional platforms)

### 1.6 Target Users
- **Equipment Owners**: Individuals or businesses with underutilized assets
- **Renters**: Individuals or businesses needing temporary equipment access
- **Investors**: Users seeking fractional ownership opportunities
- **Validators**: Community members who verify asset condition and resolve disputes
- **Insurance Providers**: Third-party entities offering coverage options

---

## 2. Core Features Breakdown

### 2.1 Asset Tokenization

#### Purpose
Transform physical equipment into verifiable digital tokens representing ownership rights.

#### Key Components
- **Asset Registration**: Owners submit equipment details, photos, and documentation
- **NFT Minting**: Each asset becomes a unique SIP-009 compliant NFT
- **Metadata Storage**: IPFS stores images, manuals, and verification documents
- **Ownership Proof**: Blockchain record of asset ownership and transfer history
- **Asset Categories**: Heavy machinery, vehicles, construction equipment, tech equipment, agricultural tools

#### Functionality Details
- Owners provide asset information including make, model, year, serial number, purchase price
- Upload multiple images showing current condition from various angles
- Attach ownership documents, purchase receipts, or lease agreements
- Set initial valuation and depreciation schedule
- Define maintenance history and service records
- Smart contract mints NFT with IPFS hash references
- Token becomes tradeable and fractionizable immediately upon minting

### 2.2 Peer-to-Peer Rental Marketplace

#### Purpose
Connect equipment owners with renters through a trustless marketplace with automated escrow.

#### Key Components
- **Listing Management**: Owners set rental terms, pricing, and availability
- **Search and Discovery**: Renters browse available equipment by category, location, price
- **Booking System**: Calendar-based availability with instant or owner-approved bookings
- **Smart Contract Escrow**: Automated payment holding and release
- **Rental Agreements**: On-chain rental terms with dispute resolution clauses

#### Functionality Details
- Owners list assets with daily/weekly/monthly rates
- Set minimum rental periods and advance booking requirements
- Define geographic restrictions and delivery options
- Renters search with filters for category, price range, location, ratings
- Submit rental requests with desired dates and use case
- Security deposit held in escrow (20-40% of rental value)
- Rental payment locked in contract until completion
- Automatic fund release upon successful return
- Dispute mechanism if issues arise

### 2.3 Fractional Ownership Mechanisms

#### Purpose
Enable multiple investors to co-own expensive equipment and share rental revenue.

#### Key Components
- **Token Fractionalization**: Split single asset NFT into fungible tokens (SIP-010)
- **Ownership Percentage**: Each fraction represents proportional ownership
- **Governance Rights**: Token holders vote on rental terms and major decisions
- **Secondary Market**: Trade fractional tokens on DEX or internal marketplace
- **Buyout Mechanism**: Majority token holders can force buyout of minority holders

#### Functionality Details
- Original owner decides fractionalization ratio (e.g., 1 NFT = 1000 tokens)
- Minimum investment threshold set per asset (e.g., minimum 10 tokens)
- Each token represents voting power in asset governance
- Owners vote on: rental pricing, asset sale, major repairs, insurance coverage
- Fractional tokens tradeable on secondary market
- Price discovery through supply and demand
- Liquidity pools can be created for high-value assets
- Majority holders (>66%) can initiate asset sale with fair price determined by oracle

### 2.4 Usage-Based Revenue Distribution

#### Purpose
Automatically distribute rental income to all token holders proportional to ownership stakes.

#### Key Components
- **Revenue Collection**: Smart contract receives rental payments
- **Platform Fee Deduction**: Protocol takes small fee (3-5%)
- **Proportional Distribution**: Revenue split based on token holdings
- **Automatic Payouts**: Funds distributed immediately after rental completion
- **Reinvestment Options**: Token holders can auto-compound earnings

#### Functionality Details
- Rental payment flows to revenue distribution contract
- Platform deducts fee (e.g., 4% to treasury)
- Maintenance reserve fund set aside (e.g., 10% of revenue)
- Remaining 86% distributed to token holders
- Distribution calculated: (user_tokens / total_tokens) × available_revenue
- Instant STX payment to each holder's wallet
- Optional: Auto-stake earnings for compound growth
- Transparent revenue history viewable on-chain
- Monthly/quarterly revenue reports generated automatically

### 2.5 Reputation and Insurance Systems

#### Reputation System

##### Purpose
Build trust through transparent performance tracking for both owners and renters.

##### Key Components
- **Rating Mechanism**: 5-star rating system post-rental
- **Review System**: Written feedback stored on-chain
- **Performance Metrics**: On-time delivery, asset condition, communication
- **Reputation Score**: Algorithmic calculation based on history
- **Badge System**: Achievement badges for milestone completions

##### Functionality Details
- Both parties rate each other after rental completion
- Ratings immutable once submitted (prevents manipulation)
- Reviews include: asset condition, cleanliness, owner responsiveness, renter care
- Reputation score calculated from: total rentals, average rating, dispute history
- Badges earned for: 10/50/100 successful rentals, zero disputes, perfect 5.0 rating
- High reputation users get: priority listings, lower insurance premiums, rental discounts
- Low reputation triggers: mandatory insurance, higher deposits, restricted access

#### Insurance System

##### Purpose
Protect both owners and renters from damage, theft, or disputes through pooled risk mechanisms.

##### Key Components
- **Damage Insurance**: Covers accidental damage during rental period
- **Theft Protection**: Compensation if asset is stolen while rented
- **Liability Coverage**: Protection against third-party claims
- **Insurance Pool**: Community-funded reserve for claims
- **Risk Assessment**: Premium calculation based on asset value and renter reputation

##### Functionality Details
- Mandatory insurance for all rentals
- Premium calculated: base_rate × asset_value × risk_multiplier
- Risk factors: renter reputation, asset category, rental duration, location
- Insurance payment added to rental cost automatically
- Claims submitted through dispute resolution system
- Validator network assesses damage and approves claims
- Payouts processed automatically from insurance pool
- Pool replenished through premiums and staking rewards
- Optional: Third-party insurance provider integration for high-value assets

---

## 3. Clarity Smart Contract Architecture

### 3.1 Contract Overview

FlexLease will consist of six primary Clarity smart contracts, each handling specific protocol functionality. All contracts will be deployed on the Stacks blockchain and interact with each other through contract calls.

### 3.2 Core Contracts

#### 3.2.1 Asset Registry Contract (asset-registry.clar)

**Purpose**: Central registry for all tokenized assets, manages asset creation, metadata, and ownership tracking.

**Responsibilities**:
- Mint asset NFTs (SIP-009 compliant)
- Store asset metadata and IPFS hash references
- Track ownership and transfer history
- Manage asset status (available, rented, maintenance, retired)
- Handle asset verification and validation

**Data Maps**:
- `assets`: Maps asset-id to asset details (owner, category, valuation, status, mint-date)
- `asset-metadata`: Maps asset-id to IPFS hashes (images, documents, certifications)
- `asset-categories`: Maps category-id to category name and requirements
- `owner-assets`: Maps principal to list of owned asset-ids
- `asset-verification`: Maps asset-id to verification status and validator

**Data Variables**:
- `asset-counter`: uint tracking total assets minted
- `platform-fee`: uint representing platform fee percentage (default 400 basis points = 4%)
- `contract-owner`: principal of contract administrator
- `paused`: boolean for emergency pause functionality

**Public Functions Needed**:
- `mint-asset`: Create new asset NFT with metadata
- `update-asset-metadata`: Modify IPFS hash references
- `transfer-asset`: Transfer ownership to new principal
- `fractionalize-asset`: Convert NFT to fractional tokens
- `update-asset-status`: Change status (available/rented/maintenance)
- `set-asset-valuation`: Update current market value
- `retire-asset`: Mark asset as permanently removed

**Read-Only Functions Needed**:
- `get-asset-details`: Retrieve complete asset information
- `get-asset-owner`: Return current owner principal
- `get-asset-metadata`: Return IPFS hashes
- `get-assets-by-category`: List all assets in category
- `get-owner-assets`: List all assets owned by principal
- `get-asset-count`: Return total assets minted

#### 3.2.2 Fractional Ownership Contract (fractional-ownership.clar)

**Purpose**: Manages the fractionalization of assets into fungible tokens (SIP-010 compliant) and handles governance.

**Responsibilities**:
- Convert asset NFTs into fractional tokens
- Manage token distribution and transfers
- Implement governance voting mechanisms
- Handle buyout procedures
- Track ownership percentages

**Data Maps**:
- `fractional-assets`: Maps asset-id to fractionalization details (total-supply, active-tokens)
- `token-balances`: Maps (asset-id, principal) to token balance
- `governance-proposals`: Maps proposal-id to proposal details and voting results
- `votes`: Maps (proposal-id, principal) to vote choice
- `buyout-offers`: Maps asset-id to active buyout offer details

**Data Variables**:
- `minimum-fractionalization`: uint representing minimum tokens per asset (default 100)
- `governance-threshold`: uint representing voting threshold percentage (default 6600 = 66%)
- `proposal-counter`: uint tracking total governance proposals

**Public Functions Needed**:
- `fractionalize`: Split asset NFT into fungible tokens
- `distribute-tokens`: Allocate tokens to initial investors
- `transfer-tokens`: SIP-010 transfer implementation
- `create-proposal`: Submit governance proposal
- `cast-vote`: Vote on active proposal
- `execute-proposal`: Execute approved proposal
- `initiate-buyout`: Start buyout process for minority holders
- `accept-buyout`: Minority holder accepts buyout offer

**Read-Only Functions Needed**:
- `get-token-balance`: Return user's token balance for asset
- `get-ownership-percentage`: Calculate percentage owned
- `get-fractional-details`: Return fractionalization information
- `get-proposal-status`: Check proposal state and results
- `get-voting-power`: Calculate user's voting power
- `is-fractionalized`: Check if asset is fractionalized

#### 3.2.3 Rental Marketplace Contract (rental-marketplace.clar)

**Purpose**: Core rental functionality including listings, bookings, escrow, and rental execution.

**Responsibilities**:
- Manage asset listings and availability
- Process rental bookings and reservations
- Handle escrow for rental payments and deposits
- Execute rental agreements
- Track rental history and current rentals

**Data Maps**:
- `listings`: Maps listing-id to listing details (asset-id, daily-rate, terms, status)
- `bookings`: Maps booking-id to booking details (listing-id, renter, dates, payment)
- `rental-agreements`: Maps agreement-id to active rental terms
- `escrow-balances`: Maps agreement-id to escrowed funds (payment + deposit)
- `rental-calendar`: Maps (asset-id, date) to availability status
- `rental-history`: Maps asset-id to list of completed rental-ids

**Data Variables**:
- `listing-counter`: uint tracking total listings
- `booking-counter`: uint tracking total bookings
- `minimum-rental-period`: uint minimum rental days (default 1)
- `maximum-advance-booking`: uint maximum days in advance (default 365)
- `deposit-percentage`: uint deposit as percentage of rental value (default 3000 = 30%)

**Public Functions Needed**:
- `create-listing`: List asset for rent with terms
- `update-listing`: Modify rental rates or availability
- `deactivate-listing`: Remove listing from marketplace
- `create-booking`: Renter submits rental request
- `approve-booking`: Owner approves rental request
- `reject-booking`: Owner rejects rental request
- `start-rental`: Execute rental agreement and lock escrow
- `complete-rental`: End rental and release funds
- `cancel-booking`: Cancel before rental start
- `extend-rental`: Extend active rental period

**Read-Only Functions Needed**:
- `get-listing-details`: Return listing information
- `get-available-assets`: List all available assets
- `check-availability`: Verify dates available for asset
- `get-booking-details`: Return booking information
- `get-active-rentals`: List ongoing rentals
- `get-rental-history`: Return completed rentals for asset
- `calculate-rental-cost`: Compute total cost for dates

#### 3.2.4 Revenue Distribution Contract (revenue-distribution.clar)

**Purpose**: Automatically distribute rental income to all stakeholders based on ownership and protocol rules.

**Responsibilities**:
- Receive rental payments from marketplace contract
- Calculate and deduct platform fees
- Distribute revenue to token holders proportionally
- Manage maintenance reserve funds
- Track revenue history and payments

**Data Maps**:
- `revenue-pools`: Maps asset-id to accumulated revenue
- `distributions`: Maps distribution-id to distribution details
- `payout-history`: Maps (asset-id, principal) to total earnings
- `maintenance-reserves`: Maps asset-id to reserved maintenance funds
- `pending-withdrawals`: Maps principal to withdrawable balance

**Data Variables**:
- `platform-fee-percentage`: uint platform fee (default 400 = 4%)
- `maintenance-reserve-percentage`: uint maintenance reserve (default 1000 = 10%)
- `treasury-address`: principal receiving platform fees
- `distribution-counter`: uint tracking total distributions

**Public Functions Needed**:
- `receive-rental-payment`: Accept payment from marketplace contract
- `distribute-revenue`: Calculate and distribute earnings to holders
- `withdraw-earnings`: User withdraws accumulated earnings
- `allocate-maintenance-fund`: Set aside funds for repairs
- `withdraw-maintenance-fund`: Owner withdraws for approved repairs
- `compound-earnings`: Auto-reinvest earnings into more tokens

**Read-Only Functions Needed**:
- `get-revenue-pool`: Return accumulated revenue for asset
- `get-user-earnings`: Calculate pending earnings for user
- `get-distribution-history`: Return past distributions
- `get-maintenance-reserve`: Return reserved funds for asset
- `calculate-distribution`: Preview distribution amounts
- `get-total-distributed`: Return lifetime distributions for asset

#### 3.2.5 Reputation Contract (reputation.clar)

**Purpose**: Track and manage reputation scores, ratings, and reviews for all platform participants.

**Responsibilities**:
- Record ratings and reviews post-rental
- Calculate reputation scores algorithmically
- Award achievement badges
- Track performance metrics
- Manage reputation-based privileges

**Data Maps**:
- `user-reputation`: Maps principal to reputation score and stats
- `ratings`: Maps (agreement-id, principal) to rating details
- `reviews`: Maps review-id to review content and IPFS hash
- `badges`: Maps (principal, badge-type) to badge earned status
- `dispute-history`: Maps principal to list of dispute-ids

**Data Variables**:
- `minimum-reputation-score`: uint minimum score to participate (default 0)
- `excellent-reputation-threshold`: uint score for premium status (default 8500 = 4.25/5)
- `review-counter`: uint tracking total reviews

**Public Functions Needed**:
- `submit-rating`: Rate counterparty after rental (1-5 stars)
- `submit-review`: Write review with IPFS hash
- `calculate-reputation`: Update user's reputation score
- `award-badge`: Grant achievement badge
- `revoke-badge`: Remove badge for policy violation
- `flag-user`: Report suspicious behavior

**Read-Only Functions Needed**:
- `get-reputation-score`: Return user's current reputation
- `get-user-stats`: Return rental count, average rating, completion rate
- `get-ratings`: Return all ratings received by user
- `get-reviews`: Return review history for user
- `get-badges`: Return all badges earned by user
- `check-reputation-requirement`: Verify if user meets threshold

#### 3.2.6 Insurance Pool Contract (insurance-pool.clar)

**Purpose**: Manage insurance premiums, claims, and payouts for rental protection.

**Responsibilities**:
- Calculate insurance premiums based on risk factors
- Collect premiums and build reserve pool
- Process damage and theft claims
- Execute payouts for approved claims
- Integrate with validator network for claim assessment

**Data Maps**:
- `insurance-policies`: Maps agreement-id to policy details and coverage
- `claims`: Maps claim-id to claim details, evidence, and status
- `pool-reserves`: Maps asset-category to available insurance funds
- `premium-history`: Maps principal to total premiums paid
- `claim-history`: Maps principal to list of past claims

**Data Variables**:
- `base-premium-rate`: uint base insurance rate (default 300 = 3%)
- `pool-balance`: uint total funds in insurance pool
- `claim-counter`: uint tracking total claims
- `maximum-claim-amount`: uint per-claim limit

**Public Functions Needed**:
- `calculate-premium`: Compute insurance cost for rental
- `collect-premium`: Receive premium payment
- `file-claim`: Submit damage or theft claim
- `submit-claim-evidence`: Upload supporting documentation (IPFS)
- `approve-claim`: Validator approves claim payout
- `reject-claim`: Validator rejects fraudulent claim
- `process-payout`: Execute approved claim payment
- `contribute-to-pool`: Users stake into insurance pool for yield

**Read-Only Functions Needed**:
- `get-premium-quote`: Preview insurance cost
- `get-policy-details`: Return coverage information
- `get-claim-status`: Check claim progress
- `get-pool-balance`: Return available insurance funds
- `get-claim-history`: Return user's past claims
- `calculate-risk-score`: Compute user's risk profile

### 3.3 Contract Interaction Flow

**Asset Creation Flow**:
1. User calls `mint-asset` on Asset Registry Contract
2. Contract validates inputs and mints SIP-009 NFT
3. Metadata stored with IPFS hash reference
4. Owner can call `fractionalize-asset` on Asset Registry
5. Asset Registry calls Fractional Ownership Contract to create tokens
6. Tokens distributed to initial investors

**Rental Flow**:
1. Owner calls `create-listing` on Rental Marketplace Contract
2. Renter calls `create-booking` with desired dates
3. Owner calls `approve-booking`
4. Marketplace calls Insurance Pool to `calculate-premium`
5. Renter calls `start-rental` with payment + deposit + premium
6. Funds locked in escrow, premium sent to Insurance Pool
7. Upon completion, renter/owner calls `complete-rental`
8. Marketplace calls Revenue Distribution to `distribute-revenue`
9. Both parties call `submit-rating` on Reputation Contract
10. Escrow released based on rental outcome

**Claim Flow**:
1. User calls `file-claim` on Insurance Pool Contract
2. Uploads evidence via `submit-claim-evidence` (IPFS)
3. Validator network reviews claim (off-chain coordination)
4. Validator calls `approve-claim` or `reject-claim`
5. If approved, Insurance Pool calls `process-payout`
6. Funds transferred from pool to claimant

---

## 4. Frontend Architecture Using Vite

### 4.1 Framework Selection: React

**Rationale**: React chosen for its mature ecosystem, excellent Stacks integration libraries, and large developer community.

**Key Libraries**:
- **React 18+**: Core framework
- **Vite**: Build tool and dev server
- **@stacks/connect**: Wallet connection and authentication
- **@stacks/transactions**: Transaction building and broadcasting
- **@stacks/network**: Network configuration
- **@stacks/storage**: Gaia storage integration (if needed)
- **React Router**: Client-side routing
- **Zustand or Jotai**: Lightweight state management
- **TanStack Query**: Server state and caching
- **Tailwind CSS**: Utility-first styling with green/black theme
- **ipfs-http-client**: IPFS interaction
- **date-fns**: Date manipulation for bookings
- **react-hook-form**: Form handling and validation

### 4.2 Project Structure

```
flexlease-frontend/
├── public/
│   ├── assets/
│   │   ├── logo.svg
│   │   ├── icons/
│   │   └── images/
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.jsx
│   │   │   ├── Card.jsx
│   │   │   ├── Input.jsx
│   │   │   ├── Modal.jsx
│   │   │   ├── Spinner.jsx
│   │   │   └── Toast.jsx
│   │   ├── layout/
│   │   │   ├── Header.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── Sidebar.jsx
│   │   │   └── Layout.jsx
│   │   ├── asset/
│   │   │   ├── AssetCard.jsx
│   │   │   ├── AssetDetails.jsx
│   │   │   ├── AssetForm.jsx
│   │   │   ├── AssetGallery.jsx
│   │   │   └── FractionalizationPanel.jsx
│   │   ├── rental/
│   │   │   ├── RentalCard.jsx
│   │   │   ├── BookingForm.jsx
│   │   │   ├── RentalCalendar.jsx
│   │   │   ├── RentalAgreement.jsx
│   │   │   └── ActiveRentals.jsx
│   │   ├── marketplace/
│   │   │   ├── SearchBar.jsx
│   │   │   ├── FilterPanel.jsx
│   │   │   ├── ListingGrid.jsx
│   │   │   └── CategoryFilter.jsx
│   │   ├── reputation/
│   │   │   ├── RatingStars.jsx
│   │   │   ├── ReviewForm.jsx
│   │   │   ├── ReputationScore.jsx
│   │   │   └── BadgeDisplay.jsx
│   │   ├── revenue/
│   │   │   ├── EarningsCard.jsx
│   │   │   ├── RevenueChart.jsx
│   │   │   └── WithdrawPanel.jsx
│   │   ├── insurance/
│   │   │   ├── PremiumCalculator.jsx
│   │   │   ├── ClaimForm.jsx
│   │   │   └── ClaimStatus.jsx
│   │   └── wallet/
│   │       ├── ConnectWallet.jsx
│   │       ├── WalletInfo.jsx
│   │       └── TransactionStatus.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Marketplace.jsx
│   │   ├── AssetDetail.jsx
│   │   ├── CreateAsset.jsx
│   │   ├── MyAssets.jsx
│   │   ├── MyRentals.jsx
│   │   ├── Dashboard.jsx
│   │   ├── Profile.jsx
│   │   └── NotFound.jsx
│   ├── hooks/
│   │   ├── useWallet.js
│   │   ├── useContract.js
│   │   ├── useIPFS.js
│   │   ├── useAssets.js
│   │   ├── useRentals.js
│   │   ├── useReputation.js
│   │   └── useRevenue.js
│   ├── services/
│   │   ├── stacksService.js
│   │   ├── ipfsService.js
│   │   ├── contractService.js
│   │   └── validationService.js
│   ├── store/
│   │   ├── walletStore.js
│   │   ├── assetStore.js
│   │   └── uiStore.js
│   ├── utils/
│   │   ├── formatters.js
│   │   ├── validators.js
│   │   ├── constants.js
│   │   └── helpers.js
│   ├── contracts/
│   │   ├── asset-registry.ts
│   │   ├── fractional-ownership.ts
│   │   ├── rental-marketplace.ts
│   │   ├── revenue-distribution.ts
│   │   ├── reputation.ts
│   │   └── insurance-pool.ts
│   ├── styles/
│   │   ├── global.css
│   │   └── theme.js
│   ├── App.jsx
│   ├── main.jsx
│   └── router.jsx
├── .env.example
├── .gitignore
├── index.html
├── package.json
├── tailwind.config.js
├── vite.config.js
└── README.md
```

### 4.3 Component Architecture

#### 4.3.1 Common Components

**Button Component**
- Variants: primary, secondary, danger, ghost
- Sizes: small, medium, large
- States: default, loading, disabled
- Green accent on hover for primary buttons

**Card Component**
- Consistent container for content sections
- Dark background with light border
- Hover effects with subtle green glow

**Modal Component**
- Overlay backdrop with blur effect
- Centered dialog on dark background
- Close button and escape key handling

**Input Component**
- Text, number, date input variants
- Validation states and error messages
- Green focus border
- Light text on dark background

#### 4.3.2 Layout Components

**Header Component**
- FlexLease logo and branding
- Navigation menu (Home, Marketplace, My Assets, Dashboard)
- Wallet connection button
- User profile dropdown
- Responsive mobile menu

**Footer Component**
- Platform links and resources
- Social media connections
- Network status indicator
- Copyright information

**Sidebar Component**
- Dashboard navigation
- Asset management links
- Rental management
- Profile settings

#### 4.3.3 Asset Components

**AssetCard Component**
- Thumbnail image from IPFS
- Asset name and category
- Daily rental rate
- Availability status indicator
- Quick action buttons (View, Rent)
- Ownership badge if user owns tokens

**AssetDetails Component**
- Full image gallery with IPFS images
- Comprehensive specifications
- Current owner information
- Fractionalization status and ownership distribution
- Revenue history chart
- Available rental dates calendar

**AssetForm Component**
- Multi-step form for asset creation
- Basic information step
- Image upload to IPFS
- Document upload (ownership proof)
- Pricing and terms configuration
- Confirmation and minting

**FractionalizationPanel Component**
- Token supply input
- Price per token setting
- Investor allocation interface
- Preview of ownership distribution
- Execute fractionalization button

#### 4.3.4 Rental Components

**RentalCard Component**
- Asset thumbnail
- Rental dates and duration
- Rental status (pending, active, completed)
- Total cost breakdown
- Action buttons based on status

**BookingForm Component**
- Date range picker with calendar
- Rental cost calculator
- Insurance premium display
- Deposit requirement
- Terms acceptance checkbox
- Submit booking button

**RentalCalendar Component**
- Month/year navigation
- Available/unavailable date highlighting
- Selected date range display
- Price variations by date
- Holiday/peak season indicators

**ActiveRentals Component**
- List of ongoing rentals
- Countdown to return date
- Contact owner/renter button
- Extend rental option
- Complete rental button

#### 4.3.5 Marketplace Components

**SearchBar Component**
- Text search input with autocomplete
- Search button with loading state
- Recent searches dropdown
- Clear search button

**FilterPanel Component**
- Category checkboxes
- Price range slider
- Location radius selector
- Availability date filter
- Rating filter
- Sort options (price, rating, distance)

**ListingGrid Component**
- Responsive grid layout (1-4 columns based on screen size)
- Asset cards with lazy loading
- Pagination or infinite scroll
- Empty state message
- Loading skeletons

#### 4.3.6 Reputation Components

**RatingStars Component**
- Interactive star display for rating input
- Read-only star display for showing ratings
- Half-star support
- Color coding (green for high ratings)

**ReviewForm Component**
- Star rating selector
- Text area for written review
- Photo upload option (IPFS)
- Submit and cancel buttons
- Character count indicator

**ReputationScore Component**
- Large score display (out of 5.0)
- Breakdown of rating categories
- Total rental count
- Completion rate percentage
- Badge display section

#### 4.3.7 Revenue Components

**EarningsCard Component**
- Total earnings display
- Pending earnings
- Withdrawn earnings
- Asset-wise breakdown
- Withdraw button

**RevenueChart Component**
- Line chart showing earnings over time
- Asset comparison view
- Time period selector (week, month, year, all)
- Export data option

**WithdrawPanel Component**
- Available balance display
- Withdrawal amount input
- Transaction fee estimate
- Withdrawal history list
- Confirm withdrawal button

### 4.4 State Management Strategy

#### 4.4.1 Global State (Zustand/Jotai)

**Wallet Store**
- Connected wallet address
- Network (mainnet/testnet)
- STX balance
- Connection status

**Asset Store**
- User's owned assets
- User's fractional holdings
- Recently viewed assets

**UI Store**
- Theme settings (already dark with green accents)
- Modal states
- Toast notifications
- Loading states

#### 4.4.2 Server State (TanStack Query)

**Asset Queries**
- All assets list with caching
- Single asset details
- User's asset portfolio
- Marketplace listings

**Rental Queries**
- Active rentals
- Rental history
- Booking requests
- Availability calendar

**Reputation Queries**
- User reputation data
- Ratings and reviews
- Badges earned

**Revenue Queries**
- Earnings data
- Distribution history
- Pending withdrawals

### 4.5 Stacks Wallet Integration

#### 4.5.1 Wallet Connection Flow

**Initial Connection**:
1. User clicks "Connect Wallet" button
2. Detect available Stacks wallets (Hiro, Leather, Xverse)
3. Show wallet selection modal
4. User selects preferred wallet
5. Wallet prompts for authentication
6. Store session and address in wallet store
7. Fetch user data (assets, rentals, reputation)

**Session Persistence**:
- Store authentication token in localStorage
- Auto-reconnect on page reload
- Session expiry handling

**Transaction Signing**:
- Build transaction using @stacks/transactions
- Call wallet to sign transaction
- User approves in wallet popup
- Broadcast transaction to network
- Poll for confirmation
- Update