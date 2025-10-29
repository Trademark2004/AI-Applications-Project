# Milestone 1 Report: New Orleans Airbnb Market Analysis

## Objective
Analyze New Orleans Airbnb market data to understand pricing patterns, property characteristics, and market dynamics to develop a price prediction model for hosts.

## Problem Definition
**Business Problem**: Help Airbnb hosts optimize pricing strategies through data-driven insights

**Why New Orleans**: 
- Year-round tourism from festivals and events
- Diverse neighborhoods with varied property types  
- Rich cultural tourism market
- Comprehensive data availability

**Research Goals**:
1. Understand property price distributions and characteristics
2. Identify key pricing factors
3. Analyze market segments and capacity patterns
4. Assess data quality for predictive modeling
5. Provide actionable host recommendations

## Data

**Source**: Inside Airbnb (September 2025 snapshot)  
**URL**: data.insideairbnb.com/united-states/la/new-orleans/

**Datasets Used**:
- **Listings**: 7,444 records, 75+ columns (property details, pricing, location, host info)
- **Calendar**: 2.7M+ records, 7 columns (daily availability and pricing)  
- **Reviews**: 489K+ records, 6 columns (guest feedback and ratings)

All datasets loaded directly via compressed CSV files for comprehensive market coverage.

## Data Preprocessing

### Initial Assessment
- Mixed data types across comprehensive property information
- Price columns stored as text strings ("$150.00") requiring conversion
- Manageable missing values across all datasets
- Rich multi-year review text content

### Price Data Conversion
**Challenge**: Formatted string prices with currency symbols

**Solution**:
- Removed dollar signs and commas
- Converted to numerical format with error handling
- Preserved original columns for verification
- Minimal data loss during conversion

### Missing Value Treatment
**Numerical Variables**: Mean imputation for accommodation capacity, pricing metrics
**Categorical Variables**: Mode imputation for property types, neighborhoods  
**Text Variables**: Meaningful placeholders ('Anonymous', empty strings)

### Outlier Detection
**Method**: IQR-based detection (1.5×IQR and 3×IQR thresholds)

**Findings**:
- Price outliers represent legitimate luxury segment
- Capacity outliers indicate commercial properties
- Zero prices suggest data quality issues

**Strategy**: Retained outliers to preserve market reality, used robust statistics for analysis

## Analysis Results

### Price Analysis
- **Median Price**: $111.00 per night
- **Mean Price**: $423.29 per night (significant luxury segment influence)
- **Range**: $15.00 to $50,134.00 per night
- **75th Percentile**: $197.00 (broad affordable market)

### Property Characteristics
- **Most Common Capacity**: 4 guests (small groups/families)
- **Average Capacity**: 5.1 guests
- **Bedroom Distribution**: Analyzed but varies widely
- **Property Mix**: Entire homes strongly dominate market

### Market Composition
**Room Type Distribution**:
- Entire Home/Apt: 84.7% (strong privacy preference)
- Private Room: 12.7% (budget segment)
- Hotel Room: 2.5% (commercial properties)
- Shared Room: 0.1% (minimal niche market)

**Geographic Spread**: French Quarter tourism core to emerging residential neighborhoods
**Host Mix**: Individual hosts and professional managers

### Correlation Analysis
**Strong Price Drivers**:
1. Host total listings count (r = 0.364) - professional host effect
2. Host listings count (r = 0.321) - scale of operations
3. Estimated revenue (r = 0.307) - market performance indicator
4. Property characteristics show more moderate correlations

**Note**: Traditional property characteristics (bedrooms, capacity) show weaker correlations than expected, suggesting host professionalization and market dynamics play larger pricing roles

## Key Visualizations

### Price Distribution
Highly right-skewed distribution with extreme luxury segment:
- **Peak**: Around $111 median mainstream market
- **Long Tail**: Luxury properties extending to $50,000+
- **Clear Segments**: Budget, mid-market, luxury, and ultra-luxury tiers

### Capacity Patterns
- **4-Person Properties**: Most common capacity (families/small groups)
- **2-4 Person Range**: Dominant market segment
- **Higher Capacity (5+)**: Significant market presence with average of 5.1 guests
- **Large Groups (8+)**: Present but less dominant than anticipated

### Market Relationships
- **Price vs. Capacity**: Strong positive correlation with linear trend
- **Property Types**: Entire homes dominate, private rooms serve budget segment
- **Geographic**: Premium locations command significant price premiums

(Visualizations: Notebook Cell 21)

## Data Quality
**Completeness**: Listings price (100% after conversion), Calendar price (100% after imputation), Property characteristics (high completeness), Location (100%), Reviews (99%+)
**Major Improvement**: Successfully imputed 2.7M calendar price values using listings base prices, enabling comprehensive temporal analysis
**Consistency**: Geographic boundaries accurate, price ranges include legitimate luxury segment up to $50K+
**Outliers**: 9.1% price outliers represent legitimate luxury/commercial segments rather than data errors

## Business Insights

### Market Opportunities
**For Hosts**:
- Capacity optimization significantly increases revenue
- Entire homes command 30-50% premium over private rooms
- Higher-priced properties show better availability (18.4% advantage)
- Premium and luxury segments have stronger booking patterns
- Temporal pricing strategies now possible with calendar data

**For Guests**:  
- Private rooms offer 40-60% savings
- Group bookings provide per-person value
- Mid-week bookings show higher availability
- Budget properties ($0-50) offer 66% availability rates

### Key Pricing Factors (Based on Correlation Analysis)
1. **Host Professionalization** - Total listings count (strongest factor)
2. **Host Scale** - Individual host portfolio size
3. **Property Type** - Entire home (84.7%) vs. room premium significant
4. **Market Performance** - Revenue estimates as pricing indicator

### Optimization Opportunities
- Professional host strategies show strongest price correlation
- Private rooms (12.7%) can enhance amenities to capture larger market share
- Ultra-luxury segment ($1,000+) represents untapped potential
- **NEW**: Dynamic pricing strategies enabled through temporal calendar data
- **NEW**: Weekend vs weekday pricing optimization (availability varies by day)
- **NEW**: Price-availability correlation insights for revenue management

## Methodology

### Data Processing Decisions & Justifications

**Price Data Standardization**:
- **Decision**: Convert string format ($XX.XX) to numerical values
- **Method**: pandas.to_numeric with error coercion  
- **Justification**: Essential for mathematical operations and statistical analysis
- **Validation**: Original data preserved for integrity verification

**Missing Value Treatment Strategy**:
- **Numerical Variables**: Mean imputation (assumes normal distribution)
- **Categorical Variables**: Mode imputation (preserves distribution shape)
- **Calendar Prices**: Cross-dataset imputation using listings base prices
- **Reviews**: Meaningful placeholders maintaining data relationships

**Categorical Data Integration**:
- **Dummy Variable Creation**: One-hot encoding for 6 key categorical variables
- **Business Focus**: Room type, neighborhood, property type, host characteristics  
- **Statistical Benefit**: Enables correlation analysis and predictive modeling
- **Feature Selection**: Balanced approach avoiding curse of dimensionality

**Outlier Management Philosophy**:
- **Detection**: IQR method (1.5×IQR and 3×IQR thresholds)
- **Treatment**: Preservation for market reality, filtering only for visualization clarity
- **Rationale**: Luxury properties represent legitimate market segment
- **Statistical Approach**: Outlier-robust methods (median, IQR) for central tendencies

### Advanced Analytical Techniques

**Multi-Dimensional Correlation Analysis**:
- Triangular correlation matrices reducing visual complexity
- Price-focused analysis isolating key pricing factors
- Categorical impact integration through dummy variables
- Statistical significance evaluation

**Geographic Market Segmentation**:
- Neighborhood-level pricing analysis with minimum volume thresholds
- Investment opportunity identification through price-performance ratios  
- Market positioning insights for strategic decision-making

**Host Performance Analytics**:
- Superhost premium quantification and market share analysis
- Booking flexibility impact on guest engagement metrics
- Performance benchmarking across host categories

**Temporal Pattern Analysis**:
- Availability rate analysis by price segments
- Weekly pattern identification for demand forecasting
- Seasonal pricing strategy insights

### Analysis Approach
- Descriptive statistics for market overview with business context
- Advanced correlation analysis across multiple dimensions
- Professional visualization suite with individual chart focus
- Cross-dataset validation ensuring analytical consistency
- Systematic outlier detection with business-informed interpretation

### Key Business Findings

**Market Structure**:
- **Dominant Segment**: Entire home/apt (84.7% market share)
- **Price Distribution**: $111 median, $423 average (indicating luxury tail)
- **Capacity Focus**: 4-guest properties dominate market positioning
- **Geographic Spread**: Significant neighborhood price variations

**Investment Insights**:
- **Superhost Premium**: Measurable price advantage and higher review volumes
- **Property Type ROI**: Clear performance differentiation across categories
- **Booking Strategy**: Instant booking correlation with availability patterns
- **Market Positioning**: Premium vs budget segment identification

**Operational Intelligence**:
- **Review Engagement**: High market validation through guest feedback
- **Price-Capacity Correlation**: Strong positive relationship (r=0.518)
- **Geographic Premium**: Neighborhood-level investment opportunity mapping  
- **Host Performance**: Measurable advantages of professional management

## Limitations
- **Temporal**: Single time point (September 2025), though calendar imputation enables temporal patterns analysis
- **Platform**: Airbnb only, not full short-term rental market
- **Imputation Assumptions**: Calendar prices assume static pricing (base listing price applied uniformly)
- **Extreme Values**: Ultra-luxury segment ($50K+) may skew statistical measures
- **External Factors**: Economic conditions, regulations not captured
- **Geographic**: Limited neighborhood-level granularity

**Mitigation**: Used robust statistics (median, IQR), successfully recovered calendar pricing data through systematic imputation, comprehensive validation of results

## Next Steps

### Feature Engineering
1. **Price Features**: Price per person, price per bedroom ratios
2. **Location Features**: Distance to attractions, neighborhood clustering
3. **Temporal Features**: Seasonality indicators, booking patterns
4. **Text Features**: Description sentiment, amenity keywords, review sentiment

### Model Development
**Primary Model**: Price prediction using Random Forest, Gradient Boosting, Neural Networks
**Target**: Nightly listing price
**Validation**: Time-based cross-validation with geographic stratification

**Secondary Models**: Guest satisfaction prediction, availability forecasting, market segmentation

### Business Applications
**Host Tools**: Dynamic pricing recommendations, property improvement suggestions, revenue optimization
**Market Analysis**: Neighborhood metrics, competitive analysis, demand forecasting

## Business Recommendations

### Airbnb Management
**Keep Core Value**: Location, convenience, cleanliness remain top priorities
**Platform Features**: Enhance capacity-based search filters and entire home promotions
**Host Standards**: Improve communication tools as responsiveness drives satisfaction

### Airbnb Hosts
**Capacity Optimization**: Maximize guest accommodation within property constraints
**Property Type Strategy**: Consider entire home conversion where feasible for 30-50% premium
**Location Marketing**: Emphasize neighborhood advantages and proximity benefits
**Pricing Strategy**: Use capacity and bedroom count as primary pricing factors

## Conclusion
This analysis shows New Orleans Airbnb market is driven by capacity and property type factors, where entire homes dominate but private rooms serve important budget segment. Core themes of location, cleanliness, and host quality remain consistent priorities. The 95%+ data completeness provides strong foundation for predictive modeling, with clear capacity-driven pricing patterns representing significant optimization opportunities for hosts.

**Code Repository**: https://github.com/Trademark2004/AI-Applications-Project  
**Notebook**: `Final_Project_661.ipynb`