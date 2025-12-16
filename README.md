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
- Update UI with transaction status
- Show success/error notifications

**Network Switching**:
- Support both mainnet and testnet
- Clear indication of current network
- Warning when switching networks
- Separate contract addresses per network

---

## 5. IPFS Integration Strategy

### 5.1 IPFS Purpose and Usage

IPFS (InterPlanetary File System) serves as the decentralized storage layer for all multimedia and document content in FlexLease. This ensures censorship resistance, content permanence, and reduces on-chain storage costs.

### 5.2 Content Stored on IPFS

**Asset Images**:
- Primary equipment photo
- Multiple angle shots (front, back, sides)
- Detail shots of important features
- Condition documentation photos
- Before/after rental photos

**Documents**:
- Ownership certificates
- Purchase receipts
- Maintenance records
- User manuals and specifications
- Insurance policies
- Inspection reports

**Review Media**:
- Photos attached to reviews
- Damage documentation for claims
- Proof of maintenance work

**Asset Metadata JSON**:
- Comprehensive asset information
- Specifications and features
- Historical data
- Links to all related IPFS content

### 5.3 IPFS Upload Flow

**Step 1: File Selection**
- User selects files through file input or drag-and-drop
- Frontend validates file types and sizes
- Image compression and optimization (max 2MB per image)
- Generate thumbnails for faster loading

**Step 2: IPFS Upload**
- Connect to IPFS node (Infura, Pinata, or local node)
- Upload file to IPFS network
- Receive Content Identifier (CID)
- Pin content to ensure availability
- Store CID temporarily in component state

**Step 3: Metadata Aggregation**
- Collect all uploaded file CIDs
- Create metadata JSON object
- Upload metadata JSON to IPFS
- Receive metadata CID

**Step 4: Blockchain Storage**
- Include metadata CID in smart contract transaction
- Call contract function with CID parameter
- CID stored in contract data map
- Permanent link between blockchain record and IPFS content

### 5.4 IPFS Retrieval Flow

**Step 1: Fetch CID from Contract**
- Query contract read-only function
- Retrieve IPFS CID for asset
- Parse CID string

**Step 2: Fetch Content from IPFS**
- Construct IPFS gateway URL (ipfs.io or Cloudflare IPFS gateway)
- Fetch content via HTTP GET request
- Implement retry logic for gateway failures
- Cache content in browser for repeat views

**Step 3: Display Content**
- Parse JSON metadata if applicable
- Render images in gallery components
- Display document links
- Lazy load images for performance

### 5.5 IPFS Hash Management in Clarity

**Storage Pattern**:
- CIDs stored as string-ascii in Clarity contracts
- Maximum length: 100 characters (sufficient for CIDv1)
- Each asset has primary metadata CID
- Additional CIDs for updates/modifications

**Contract Storage Example**:
```
Asset Metadata Map Structure:
{
  asset-id: u1,
  metadata-cid: "QmX7g8...",
  image-cids: ["QmY2h3...", "QmZ4k9..."],
  document-cids: ["QmA8m5..."],
  last-updated: u1234567890
}
```

**Update Mechanism**:
- Owner can update metadata CID
- Historical CIDs preserved in update log
- Prevents content manipulation disputes
- Immutable history of all versions

### 5.6 IPFS Gateway Strategy

**Primary Gateway**: Cloudflare IPFS Gateway
- Fast global CDN
- High availability
- HTTPS support
- URL format: `https://cloudflare-ipfs.com/ipfs/{CID}`

**Backup Gateway**: IPFS.io
- Official IPFS gateway
- Fallback if primary fails
- URL format: `https://ipfs.io/ipfs/{CID}`

**Local Node Option**:
- Power users can run local IPFS nodes
- Direct IPFS protocol access
- Faster retrieval for pinned content
- URL format: `http://localhost:8080/ipfs/{CID}`

### 5.7 Content Pinning Strategy

**Pinning Services**:
- Pinata: Primary pinning service for reliability
- Infura: Backup pinning service
- Web3.Storage: Additional redundancy

**Pinning Logic**:
- Automatically pin all uploaded content to at least 2 services
- Critical content (asset images, ownership docs) pinned to 3 services
- Monitor pin status and re-pin if unpinned
- Paid pinning plans for guaranteed availability

**Cost Optimization**:
- Free tier usage for development/testing
- Paid tiers for production
- Estimate: $10-50/month for 10GB storage with redundancy

### 5.8 IPFS Security Considerations

**Content Verification**:
- Verify CID matches content hash
- Detect content tampering attempts
- Validate file types before display
- Scan for malicious content

**Privacy Considerations**:
- All IPFS content is public by default
- Sensitive documents should be encrypted before upload
- Personal information redacted from public images
- Option for private IPFS networks for sensitive data

**Content Moderation**:
- Report mechanism for inappropriate content
- Community validators review flagged content
- Ability to update CID if content violates terms
- Legal compliance for DMCA takedowns

---

## 6. Data Structure Design

### 6.1 On-Chain Data (Clarity Contracts)

**Principle**: Store only essential, verifiable data on-chain. Minimize storage costs while ensuring data integrity.

#### Asset Registry Contract Data

**On-Chain**:
- Asset ID (uint)
- Owner principal (address)
- Asset category (uint mapped to enum)
- Current valuation (uint in micro-STX)
- Status (uint: 0=available, 1=rented, 2=maintenance, 3=retired)
- Metadata CID (string-ascii)
- Mint block height (uint)
- Fractional status (bool)
- Verification status (bool)
- Validator principal (optional)

**Off-Chain (IPFS)**:
- Asset name and description
- Detailed specifications
- Images (multiple URLs)
- Purchase receipts
- Ownership documents
- Maintenance history
- Serial numbers
- Manufacturer information

#### Fractional Ownership Contract Data

**On-Chain**:
- Asset ID (uint)
- Total token supply (uint)
- Token symbol (string-ascii)
- Token balances per principal (map)
- Governance proposal details
- Voting records
- Proposal execution status

**Off-Chain (IPFS)**:
- Detailed proposal descriptions
- Supporting documents
- Discussion threads
- Vote explanations

#### Rental Marketplace Contract Data

**On-Chain**:
- Listing ID (uint)
- Asset ID (uint)
- Daily rate (uint in micro-STX)
- Minimum rental period (uint days)
- Security deposit percentage (uint)
- Listing status (uint: active/paused/closed)
- Booking ID (uint)
- Renter principal
- Start date (uint timestamp)
- End date (uint timestamp)
- Total payment (uint)
- Escrow balance (uint)
- Rental status (uint: pending/active/completed/disputed)

**Off-Chain (IPFS)**:
- Detailed rental terms and conditions
- Usage restrictions
- Location details and coordinates
- Delivery/pickup instructions
- Additional photos
- Rental agreement PDF

#### Revenue Distribution Contract Data

**On-Chain**:
- Asset ID (uint)
- Revenue pool balance (uint)
- Maintenance reserve (uint)
- Distribution ID (uint)
- Distribution amount per token (uint)
- Timestamp (uint)
- User withdrawal balances (map: principal -> uint)
- Total distributed (uint)

**Off-Chain (IPFS)**:
- Detailed revenue reports
- Expense breakdowns
- Maintenance receipts
- Distribution history exports

#### Reputation Contract Data

**On-Chain**:
- User principal (address)
- Reputation score (uint: 0-10000, representing 0.00-5.00)
- Total rentals (uint)
- Successful completions (uint)
- Average rating (uint)
- Rating details (map: agreement-id -> uint)
- Review CIDs (list of string-ascii)
- Badge list (list of uint badge-type)
- Dispute count (uint)
- Last updated (uint timestamp)

**Off-Chain (IPFS)**:
- Full review text
- Review photos
- Detailed performance metrics
- Communication quality ratings
- Badge images and descriptions

#### Insurance Pool Contract Data

**On-Chain**:
- Policy ID (uint)
- Agreement ID (uint)
- Premium amount (uint)
- Coverage amount (uint)
- Policy status (uint)
- Claim ID (uint)
- Claim amount (uint)
- Claim status (uint: pending/approved/rejected)
- Evidence CIDs (list)
- Validator approvals (map)
- Payout amount (uint)
- Pool balance (uint per category)

**Off-Chain (IPFS)**:
- Claim descriptions
- Damage photos
- Repair estimates
- Third-party assessment reports
- Communication logs

### 6.2 Off-Chain Data Storage Strategy

**IPFS Content Structure**:

**Asset Metadata JSON**:
```json
{
  "name": "CAT 320 Excavator",
  "description": "2020 Caterpillar 320 excavator...",
  "category": "heavy-machinery",
  "specifications": {
    "make": "Caterpillar",
    "model": "320",
    "year": 2020,
    "serialNumber": "CAT0320WXYZ",
    "operatingWeight": "20000 kg",
    "enginePower": "121 kW"
  },
  "images": [
    "QmImageCID1",
    "QmImageCID2",
    "QmImageCID3"
  ],
  "documents": {
    "ownership": "QmOwnershipCID",
    "purchase": "QmPurchaseCID",
    "manual": "QmManualCID"
  },
  "location": {
    "city": "Denver",
    "state": "CO",
    "coordinates": "39.7392,-104.9903"
  },
  "maintenanceHistory": [
    {
      "date": "2024-03-15",
      "type": "routine",
      "description": "Oil change and filter replacement",
      "receipt": "QmMaintenanceCID1"
    }
  ]
}
```

**Review JSON**:
```json
{
  "rating": 5,
  "reviewText": "Excellent equipment, well maintained...",
  "categories": {
    "condition": 5,
    "cleanliness": 5,
    "communication": 5,
    "valueForMoney": 4
  },
  "photos": ["QmReviewPhoto1", "QmReviewPhoto2"],
  "timestamp": 1701234567,
  "verified": true
}
```

### 6.3 Data Synchronization Strategy

**Blockchain as Source of Truth**:
- Smart contract state is canonical
- IPFS content referenced by on-chain CIDs
- Frontend caches both blockchain and IPFS data
- Periodic sync to ensure consistency

**Frontend Caching**:
- TanStack Query caches contract reads (5-minute stale time)
- IPFS content cached in browser (1-day stale time)
- IndexedDB for offline support (optional)
- Service Worker for asset images (optional)

**Real-Time Updates**:
- Subscribe to blockchain events for owned assets
- WebSocket connection for rental status changes
- Push notifications for important events
- Automatic UI refresh on state changes

---

## 7. User Roles and Permissions

### 7.1 Role Definitions

#### 7.1.1 Asset Owner

**Primary Responsibilities**:
- Create and manage asset listings
- Set rental terms and pricing
- Approve or reject booking requests
- Maintain asset condition
- Handle renter communications
- Process insurance claims for damage

**Permissions**:
- Mint new asset NFTs
- Fractionalize owned assets
- Create rental listings
- Approve/reject bookings
- Update asset metadata and pricing
- Withdraw rental revenue
- Submit maintenance fund requests
- Rate and review renters
- Initiate dispute resolution

**Restrictions**:
- Cannot rent own assets
- Cannot manipulate reputation scores
- Cannot withdraw escrowed funds prematurely
- Must maintain minimum reputation for premium features

#### 7.1.2 Renter

**Primary Responsibilities**:
- Search and discover available equipment
- Submit rental booking requests
- Pay rental fees and deposits
- Use equipment responsibly per terms
- Return equipment on time and in good condition
- Report damages immediately

**Permissions**:
- Browse marketplace
- Submit booking requests
- Pay for rentals
- Extend active rentals
- Complete rental checkout
- Rate and review owners
- File insurance claims for disputes
- View rental history

**Restrictions**:
- Must have minimum reputation score to rent high-value assets
- Cannot cancel rental after start without penalty
- Cannot sublease rented equipment
- Must comply with usage restrictions
- Limited to maximum concurrent rentals based on reputation

#### 7.1.3 Fractional Owner/Investor

**Primary Responsibilities**:
- Purchase fractional tokens of assets
- Participate in governance voting
- Monitor asset performance
- Earn passive income from rentals

**Permissions**:
- Buy/sell fractional tokens
- Vote on governance proposals
- Receive proportional rental revenue
- View detailed asset analytics
- Propose asset sale or major changes
- Withdraw accumulated earnings

**Restrictions**:
- Voting power proportional to tokens held
- Cannot unilaterally make asset decisions
- Subject to lockup periods (optional)
- Must hold minimum tokens to vote
- Cannot force sale without majority approval

#### 7.1.4 Validator

**Primary Responsibilities**:
- Verify asset authenticity and condition
- Review insurance claims
- Mediate disputes between parties
- Ensure platform policy compliance
- Provide expert assessments

**Permissions**:
- Access to all asset documentation
- Approve/reject asset verifications
- Approve/reject insurance claims
- Issue reputation penalties
- Access dispute resolution system
- Earn validation rewards

**Requirements**:
- Staked collateral (e.g., 10,000 STX)
- Proven expertise in asset category
- High reputation score (4.5+)
- Community election or platform appointment
- Regular activity requirements

**Restrictions**:
- Cannot validate own assets or rentals
- Cannot participate in rentals while validating
- Collateral slashed for fraudulent decisions
- Term limits and performance reviews

#### 7.1.5 Platform Administrator

**Primary Responsibilities**:
- Maintain platform infrastructure
- Update smart contracts (via governance)
- Manage emergency situations
- Handle legal compliance
- Moderate content
- Resolve critical disputes

**Permissions**:
- Pause/unpause contracts in emergencies
- Update platform fee parameters
- Add/remove validator approvals
- Remove illegal content
- Access all platform data for audits
- Implement governance decisions

**Restrictions**:
- Cannot access user funds directly
- Cannot manipulate user reputations
- Subject to multi-sig requirements
- Actions logged and auditable
- Term limits via governance

### 7.2 Permission Matrix

| Action | Owner | Renter | Investor | Validator | Admin |
|--------|-------|--------|----------|-----------|-------|
| Mint Asset | ✅ | ❌ | ❌ | ❌ | ❌ |
| Create Listing | ✅ | ❌ | ⚠️* | ❌ | ❌ |
| Book Rental | ⚠️** | ✅ | ✅ | ❌ | ❌ |
| Approve Booking | ✅ | ❌ | ⚠️* | ❌ | ❌ |
| Complete Rental | ✅ | ✅ | ❌ | ❌ | ❌ |
| Rate User | ✅ | ✅ | ❌ | ❌ | ❌ |
| File Claim | ✅ | ✅ | ✅ | ❌ | ❌ |
| Approve Claim | ❌ | ❌ | ❌ | ✅ | ⚠️*** |
| Vote on Proposal | ⚠️* | ❌ | ✅ | ❌ | ❌ |
| Fractionalize Asset | ✅ | ❌ | ❌ | ❌ | ❌ |
| Buy Tokens | ✅ | ✅ | ✅ | ✅ | ✅ |
| Withdraw Revenue | ✅ | ❌ | ✅ | ❌ | ❌ |
| Verify Asset | ❌ | ❌ | ❌ | ✅ | ✅ |
| Pause Contract | ❌ | ❌ | ❌ | ❌ | ✅ |

*If holding fractional tokens of the asset
**Cannot rent own assets
***Only in emergency situations

### 7.3 Reputation-Based Permissions

**Tier 1: New User (0-3.0 rating)**
- Limited to assets under $500 value
- Maximum 1 active rental
- Higher insurance premiums (+50%)
- Higher security deposits (+50%)
- Cannot participate in governance

**Tier 2: Established User (3.0-4.0 rating)**
- Access to assets up to $2,500
- Maximum 3 active rentals
- Standard insurance premiums
- Standard security deposits
- Can vote on governance (minimum tokens required)

**Tier 3: Trusted User (4.0-4.5 rating)**
- Access to assets up to $10,000
- Maximum 5 active rentals
- Reduced insurance premiums (-20%)
- Reduced security deposits (-20%)
- Enhanced governance voting power (1.5x)
- Eligible for validator role

**Tier 4: Premium User (4.5-5.0 rating)**
- Unlimited asset value access
- Unlimited active rentals
- Reduced insurance premiums (-40%)
- Reduced security deposits (-40%)
- Enhanced governance voting power (2x)
- Priority listing placement
- Validator role eligibility
- Platform fee discounts (-25%)

---

## 8. User Flows and Interactions

### 8.1 Asset Listing Flow

**Step 1: Asset Creation**
1. Owner clicks "List Equipment" button
2. Connects wallet if not already connected
3. Selects asset category from dropdown
4. Fills out asset information form:
   - Name (e.g., "2020 CAT 320 Excavator")
   - Description (detailed text)
   - Specifications (make, model, year, serial number)
   - Purchase price and current valuation
   - Location (city, state)

**Step 2: Image Upload**
1. Clicks "Add Photos" button
2. Selects multiple images from device (min 3, max 10)
3. Frontend compresses images to max 2MB each
4. Images uploaded to IPFS sequentially
5. Progress bar shows upload status
6. IPFS CIDs stored temporarily in form state
7. Thumbnail previews displayed

**Step 3: Document Upload**
1. Clicks "Add Documents" section
2. Uploads ownership certificate (required)
3. Uploads purchase receipt (optional)
4. Uploads maintenance records (optional)
5. Documents uploaded to IPFS
6. CIDs stored in form state

**Step 4: Create Metadata**
1. Frontend aggregates all form data
2. Creates JSON metadata object
3. Uploads metadata JSON to IPFS
4. Receives metadata CID

**Step 5: Blockchain Transaction**
1. User reviews summary of asset details
2. Clicks "Mint Asset" button
3. Frontend builds Clarity transaction calling `mint-asset`
4. Transaction includes metadata CID
5. Wallet prompts for signature
6. User approves transaction
7. Transaction broadcast to Stacks network
8. Frontend shows "Transaction Pending" status
9. Polls for transaction confirmation
10. Success notification displayed
11. Asset appears in "My Assets" page

**Step 6: Create Rental Listing (Optional)**
1. From asset detail page, click "Create Listing"
2. Set daily rental rate (STX)
3. Set minimum rental period (days)
4. Set security deposit percentage (15-50%)
5. Define availability calendar
6. Set geographic restrictions (optional)
7. Add special terms (IPFS)
8. Review and confirm
9. Sign transaction calling `create-listing`
10. Listing appears in marketplace

### 8.2 Rental Booking Flow

**Step 1: Discovery**
1. Renter visits marketplace page
2. Uses search bar or filters
3. Filters by category, price, location, dates
4. Browses asset cards in grid
5. Clicks asset for details

**Step 2: Asset Review**
1. Views full image gallery
2. Reads specifications and description
3. Checks owner reputation and reviews
4. Reviews available dates on calendar
5. Reads rental terms

**Step 3: Booking Request**
1. Clicks "Book Now" button
2. Selects start and end dates from calendar
3. System calculates:
   - Base rental cost (days × daily rate)
   - Security deposit (% of rental cost)
   - Insurance premium (based on risk factors)
   - Platform fee (4% of rental cost)
   - Total amount due
4. Reviews cost breakdown
5. Reads and accepts rental agreement
6. Clicks "Submit Booking"

**Step 4: Payment Processing**
1. Frontend builds transaction calling `create-booking`
2. Transaction includes total payment amount
3. Wallet prompts showing exact STX amount
4. User approves and signs transaction
5. Funds transferred to escrow contract
6. Booking created with "Pending Owner Approval" status
7. Owner receives notification

**Step 5: Owner Approval**
1. Owner reviews booking request
2. Checks renter reputation
3. Confirms availability
4. Clicks "Approve" or "Reject"
5. If approved:
   - Calls `approve-booking` function
   - Booking status changes to "Approved"
   - Calendar updated to block dates
   - Both parties receive confirmation
6. If rejected:
   - Calls `reject-booking` function
   - Escrow funds returned to renter
   - Booking canceled

**Step 6: Rental Start**
1. On start date, renter clicks "Start Rental"
2. Calls `start-rental` function
3. Rental status changes to "Active"
4. Owner provides equipment access details
5. Renter confirms receipt of equipment
6. Timer starts for rental duration

### 8.3 Rental Completion Flow

**Step 1: Return Process**
1. Renter returns equipment on or before end date
2. Owner inspects equipment condition
3. Compares to pre-rental photos
4. Documents any damages with photos (uploaded to IPFS)

**Step 2: Condition Assessment**
1. If equipment in good condition:
   - Owner clicks "Complete Rental - No Issues"
   - Calls `complete-rental` function
   - Full security deposit returned to renter
   - Rental payment released to revenue distribution
2. If equipment damaged:
   - Owner clicks "Complete Rental - Damage Claim"
   - Submits damage details and photos
   - Initiates insurance claim
   - Partial deposit withheld pending claim

**Step 3: Payment Distribution**
1. Revenue Distribution Contract triggered automatically
2. Platform fee deducted (4%)
3. Maintenance reserve set aside (10%)
4. Remaining amount distributed:
   - If single owner: 100% to owner
   - If fractionalized: proportional to token holdings
5. Funds instantly available for withdrawal

**Step 4: Reputation Update**
1. Both parties prompted to rate each other
2. Rating form with 5-star scale for categories:
   - Equipment condition (owner rates renter)
   - Timeliness (both parties)
   - Communication (both parties)
   - Overall experience (both parties)
3. Optional written review
4. Reviews submitted to Reputation Contract
5. Reputation scores recalculated automatically
6. Badges awarded if milestones reached

### 8.4 Dispute Resolution Flow

**Step 1: Dispute Initiation**
1. Party (owner or renter) believes rental terms violated
2. Clicks "File Dispute" from active rental page
3. Selects dispute type:
   - Equipment damage
   - Late return
   - Unauthorized use
   - Equipment malfunction
   - Communication breakdown
4. Provides detailed description
5. Uploads supporting evidence (photos, messages) to IPFS
6. Submits dispute

**Step 2: Validator Assignment**
1. System selects 3 random validators with relevant expertise
2. Validators notified of new dispute
3. Validators review:
   - Original rental agreement
   - Both parties' accounts
   - Evidence from both sides
   - Rental history and reputation
4. 48-hour review period

**Step 3: Validator Decision**
1. Each validator submits decision:
   - Favor owner
   - Favor renter
   - Split decision (partial refund/payment)
2. Majority decision prevails
3. If 2-1 split, additional validator called
4. Final decision binding

**Step 4: Resolution Execution**
1. Smart contract executes decision automatically:
   - Funds released according to ruling
   - Security deposit distributed per decision
   - Insurance claim approved/rejected
2. Both parties notified of outcome
3. Reputation impacts applied:
   - Losing party receives minor negative mark
   - False dispute filing penalized more heavily
4. Case closed and archived

### 8.5 Fractionalization Flow

**Step 1: Decision to Fractionalize**
1. Asset owner views asset detail page
2. Clicks "Fractionalize Asset" button
3. Reviews benefits and implications
4. Confirms intent to proceed

**Step 2: Configuration**
1. Sets total token supply (e.g., 1000 tokens)
2. Defines price per token (e.g., 10 STX)
3. Chooses allocation method:
   - Public sale (anyone can buy)
   - Private sale (whitelist only)
   - Combination
4. Sets vesting schedule (optional)
5. Defines minimum purchase amount
6. Reviews token economics

**Step 3: Governance Setup**
1. Configures voting parameters:
   - Quorum requirement (% of tokens must vote)
   - Approval threshold (% to pass proposal)
   - Voting period duration
2. Lists votable decisions:
   - Rental pricing changes
   - Asset sale
   - Major repairs
   - Insurance coverage
3. Reviews and confirms

**Step 4: Fractionalization Execution**
1. Clicks "Execute Fractionalization"
2. Signs transaction calling `fractionalize` function
3. Asset NFT locked in Fractional Ownership Contract
4. Fungible tokens (SIP-010) created
5. Tokens allocated to owner initially
6. Listing created on internal marketplace or DEX

**Step 5: Token Distribution**
1. Investors browse fractional opportunities
2. View asset details, revenue projections, terms
3. Purchase tokens via `buy-tokens` function
4. Tokens transferred to buyer
5. Payment sent to seller (original owner or secondary seller)
6. Ownership percentage updated automatically
7. Buyer gains governance rights immediately

### 8.6 Governance Voting Flow

**Step 1: Proposal Creation**
1. Token holder clicks "Create Proposal"
2. Selects proposal type:
   - Change rental pricing
   - Sell asset
   - Approve major repair (>$X)
   - Update insurance coverage
   - Other
3. Provides proposal title and detailed description
4. Uploads supporting documents to IPFS
5. Sets voting duration (default 7 days)
6. Requires minimum tokens to submit (e.g., 5%)

**Step 2: Proposal Submission**
1. Reviews proposal summary
2. Signs transaction calling `create-proposal`
3. Proposal ID assigned
4. Voting period begins immediately
5. All token holders notified

**Step 3: Voting Period**
1. Token holders view active proposals
2. Read proposal details and discussion
3. Cast vote: For, Against, or Abstain
4. Voting power = number of tokens held
5. Can change vote before period ends
6. Votes recorded on-chain immutably

**Step 4: Proposal Resolution**
1. Voting period expires
2. System calculates results:
   - Total votes cast
   - For vs Against percentage
   - Quorum met? (minimum participation)
   - Threshold met? (approval percentage)
3. Proposal status updated: Passed or Failed
4. If passed, enters execution queue

**Step 5: Proposal Execution**
1. Authorized party (owner or admin) clicks "Execute"
2. Calls `execute-proposal` function
3. Smart contract implements decision:
   - Updates rental pricing
   - Initiates asset sale process
   - Releases maintenance funds
   - Updates insurance coverage
4. Proposal marked as "Executed"
5. All token holders notified of changes

---

## 9. Stacks Blockchain Interaction Patterns

### 9.1 Transaction Building and Broadcasting

**Transaction Flow**:
1. Frontend prepares transaction parameters
2. Uses @stacks/transactions library to build transaction object
3. Specifies contract address, function name, and arguments
4. Sets network (mainnet/testnet)
5. Includes appropriate fee estimation
6. Requests wallet signature via @stacks/connect
7. User approves in wallet extension
8. Signed transaction broadcast to network
9. Transaction ID returned immediately

**Code Pattern** (Conceptual):
```
1. Import required functions from @stacks/transactions
2. Define contract address and function name
3. Prepare function arguments in Clarity format
4. Build PostConditions for security
5. Create transaction options object
6. Call openContractCall from @stacks/connect
7. Handle success/error callbacks
8. Update UI with transaction status
```

**Fee Estimation**:
- Query recent transaction fees via Stacks API
- Calculate based on transaction complexity
- Provide user with fee estimate before signing
- Allow advanced users to adjust fee manually
- Default to recommended fee for optimal confirmation time

### 9.2 Contract Call Patterns

**Read-Only Calls**:
- No transaction required
- Free and instant
- Query contract state
- Used for: checking balances, fetching asset details, viewing listings
- Pattern: call read-only function via Stacks API
- Cache results with TanStack Query
- Refresh on relevant state changes

**Public Function Calls**:
- Requires transaction and wallet signature
- Costs gas fees
- Modifies contract state
- Used for: minting assets, creating bookings, voting
- Pattern: build transaction → sign → broadcast → wait for confirmation
- Show pending state in UI immediately
- Poll for confirmation every 3-5 seconds
- Update UI on confirmation

### 9.3 Event Listening and Real-Time Updates

**Contract Events**:
Clarity contracts can emit print events that frontends can listen to for real-time updates.

**Key Events to Monitor**:
- `asset-minted`: New asset created
- `listing-created`: New rental listing
- `booking-created`: New rental request
- `rental-started`: Rental became active
- `rental-completed`: Rental finished
- `payment-distributed`: Revenue sent to owners
- `reputation-updated`: User score changed
- `proposal-created`: New governance vote
- `claim-filed`: Insurance claim submitted

**Listening Strategy**:
1. Subscribe to WebSocket connection with Stacks node
2. Filter events by contract address
3. Parse event data from print statements
4. Update frontend state reactively
5. Show toast notifications for important events
6. Refresh relevant queries in TanStack Query

**Polling Fallback**:
- WebSocket may not always be available
- Implement polling as fallback (every 10-30 seconds)
- Poll specific read-only functions for critical data
- More frequent polling for time-sensitive operations

### 9.4 Post Conditions

**Purpose**: Enforce safety constraints on transactions to prevent unexpected outcomes.

**Common Post Conditions**:

**STX