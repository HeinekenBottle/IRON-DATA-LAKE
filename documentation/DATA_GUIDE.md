# IRON Data Lake - AI Agent Guide

## 🎯 Purpose
This data lake contains representative samples from the IRON trading analytics platform for AI agent analysis. The data supports pattern discovery across 6 dimensions (D1-D6) of market microstructure.

## 📊 Dataset Overview

### Sample Data Structure
```
samples/
├── gold/nq_sample_2024.parquet    # NQ futures July-August 2024
├── silver/                        # Processed IRONCORE features
└── bronze/                        # Raw ingestion data
```

### Key Features (Gold Layer)
- **syn_vol**: Synthetic volume ratio - stealth activity detection (≤0.0493 = stealth)
- **price_relativity**: Multi-timeframe price relationships
- **liq_taken_15m/30m/60m**: Liquidity sweep labels (targets)
- **fvg_***: Fair value gap features (D3 dimension)
- **pll_strength**: Price level liquidity strength (D2 dimension)

## 🔍 Pattern Discovery Dimensions

**D1 Liquidity**: DTW clustering, GMM/HMM states → stealth detection
**D2 ICT Macro**: Matrix profile, cyclic patterns → macro phases
**D3 FPFVG**: PrefixSpan sequences, survival analysis → FVG motifs
**D4 News Context**: Vision extraction → news impact correlation
**D5 Weekly Profiles**: Day-of-week analysis → weekly stratification
**D6 Sequential**: PC Algorithm → causal dependencies

## 🎲 Data Usage for AI Analysis

### Stealth Pattern Analysis
```python
# Key threshold for stealth detection
stealth_events = data[data['syn_vol'] <= 0.0493]

# Cross-dimensional validation
high_conviction = data[
    (data['syn_vol'] <= 0.0493) &           # D1: Stealth
    (data['pll_strength'] > 0.7) &          # D2: Strong level
    (data['fvg_score'] > 0.5)               # D3: Active FVG
]
```

### Statistical Properties
- **Timeframe**: 1-minute bars during market hours (9:30-16:00 ET)
- **Symbols**: NQ (Nasdaq 100 E-mini futures)
- **Sample Period**: July-August 2024 (representative market conditions)
- **Feature Count**: 50+ engineered features across D1-D6 dimensions

## 🔗 Related Repositories
- **IRONDISC**: Pattern discovery algorithms that process this data
- **IRONCORE**: Feature engineering that creates gold layer from silver
- **IRONSOURCE**: Data ingestion that creates bronze/silver layers

## 📈 Expected Patterns for AI Analysis

### Volume Patterns
- Stealth accumulation: syn_vol ≤ 0.0493 (67% of significant moves)
- Volume spikes: syn_vol > 2.0 during breakouts
- Institutional flow: consistent syn_vol 0.8-1.2 ranges

### Price Action Patterns
- Liquidity sweeps: price_relativity crossing key levels
- Fair value gaps: fvg_score peaks before reversals
- Weekly cycles: different behaviors by day-of-week

### Cross-Dimensional Correlations
- D1 + D2: Stealth + strong levels = 73% accuracy for 15m sweeps
- D3 + D5: FVG + weekly regime = improved precision
- D6: Sequential dependencies enhance all other dimensions

## 🤖 AI Agent Opportunities

1. **Threshold Optimization**: Analyze syn_vol distributions for better stealth detection
2. **Feature Engineering**: Discover new patterns from existing features
3. **Cross-Reference Research**: Find academic papers on similar microstructure patterns
4. **Validation Methods**: Suggest statistical tests for pattern significance
5. **Regime Detection**: Identify market regime changes in the data

## ⚠️ Data Characteristics

- **No PII**: Market data only, no personal information
- **Representative Sample**: 2-month period captures various market conditions
- **Feature Focus**: Emphasis on derived features over raw OHLCV
- **Timezone**: All timestamps in America/New_York (market timezone)

---

*This dataset enables AI agents to understand both the sophisticated algorithms in IRONDISC and the actual market patterns they're designed to detect.*