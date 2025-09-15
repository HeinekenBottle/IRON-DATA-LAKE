# IRON Data Lake - Complete Dataset Index

## 🎯 Quick Access for AI Agents

### 🔑 Key Features Available
- **syn_vol**: Stealth volume ratio (≤0.0493 = stealth detection)
- **price_relativity**: Multi-timeframe price relationships
- **liq_taken_15m/30m/60m**: Liquidity sweep labels
- **fvg_***: Fair value gap features (D3 dimension)
- **pll_strength**: Price level liquidity strength

## 📊 Primary Datasets

### Gold Layer (Production Ready)
```
gold/
├── canonical_1m/v1.1/              # 1-minute bars with all features (syn_vol here!)
│   ├── date=2025-07-23/1m_2025-07-23.parquet
│   ├── date=2025-07-24/1m_2025-07-24.parquet
│   └── ... (daily files Jul 23 - Aug 7, 2025)
├── canonical_session/v1.1/         # Session-level aggregations
│   ├── date=2025-07-23/sessions_2025-07-23.parquet
│   └── ... (daily session files)
├── bars/symbol=NQ/                  # OHLCV bars
│   ├── jul_aug_2024.parquet
│   ├── jul_aug_2025.parquet
│   └── sample_data.parquet
├── features.parquet                 # FPFVG event features (102 events)
└── labels.parquet                   # Trading labels (liquidity sweep targets)
```

### Silver Layer (Processed)
```
silver/
└── timeline/                        # Processed timeline data
    ├── session_date=2025-07-23/timeline.parquet
    └── ... (daily timeline files)
```

### Bronze Layer (Raw Ingestion)
```
bronze/
├── events/                          # Raw market events
│   ├── session_date=2025-07-23/events.parquet
│   └── ... (daily event files)
└── session_refs/                    # Session reference data
    ├── session_date=2025-07-23/refs.parquet
    └── ... (daily reference files)
```

## 🔬 Analysis Artifacts

### IRONDISC Pattern Discovery Results
```
artifacts/irondisc/
├── dimensions/                      # D1-D6 dimensional analysis
│   ├── d1/dtw_clusters.json         # DTW clustering results
│   ├── d1_ironcore/                 # D1 IRONCORE features
│   ├── d3_fpfvg/                    # D3 Fair Value Gap patterns
│   ├── liquidity/results/           # GMM/HMM liquidity models
│   ├── macro_windows/results/       # D2 Matrix profile patterns
│   ├── news/results/                # D4 News impact analysis
│   ├── sequential/results/          # D6 PC Algorithm causal edges
│   └── weekly/results/              # D5 Weekly regime analysis
├── fusion/                          # Multi-dimensional pattern fusion
│   ├── stealth_accumulation/        # D1+D2 stealth patterns
│   ├── three_dimensional_stealth/   # D1+D2+D3 enhanced patterns
│   └── cross_dimensional/           # Synthetic cross-D patterns
├── correlation_analysis/            # Cross-feature correlations
├── environmental_intelligence/      # Market regime detection
├── rules/                          # Association rules and RF importance
└── validation/                     # Statistical validation results
```

### IRONFISH Discovery Results
```
artifacts/ironfish/
├── discovery/                       # Pattern discovery experiments
│   ├── dtw_blending/               # DTW cluster blending
│   ├── enhanced/                   # Enhanced pipeline results
│   ├── pooled/                     # Pooled window analysis
│   └── windows/                    # Daily pattern windows
└── runs/                           # Individual discovery runs
    ├── session_profile_*/          # Session profiling results
    └── discovery_*/                # Discovery algorithm outputs
```

## 🎲 Key Features for AI Analysis

### Stealth Detection (D1 Dimension)
- **Location**: `gold/canonical_1m/v1.1/date=*/1m_*.parquet`
- **Key Column**: `syn_vol` (stealth threshold: ≤0.0493)
- **Supporting**: `syn_vol_z` (z-score normalized)

### Market Microstructure Features
- **Price Relativity**: `rel_open`, `rel_high`, `rel_low`, `ratio_to_prev_*`
- **Positioning**: `pos_in_prev_*`, `pos_in_D_range`
- **Targets**: `top_target_price`, `top_target_dist`, `top_target_score`

### Liquidity Analysis
- **Labels**: `gold/labels.parquet` → `label_any_15`, `label_any_30`, `label_any_60`
- **Events**: `gold/features.parquet` → FPFVG-based features
- **Models**: `artifacts/irondisc/dimensions/liquidity/results/`

## 📈 Data Characteristics

### Temporal Coverage
- **Primary Period**: July 23 - August 7, 2025 (latest patterns)
- **Historical Sample**: July-August 2024 (in samples/)
- **Frequency**: 1-minute bars during market hours (9:30-16:00 ET)
- **Symbol**: NQ (Nasdaq 100 E-mini futures)

### Data Volume
- **Gold 1m**: ~8 rows per session per date (limited to key events)
- **Sample Data**: 13,949 1-minute bars (Jul-Aug 2024)
- **Total Files**: 150+ parquet files across all layers
- **Analysis Results**: 100+ artifact files with patterns

### Key Statistics
- **Stealth Events**: syn_vol ≤ 0.0493 (67% of significant moves)
- **Feature Count**: 30+ engineered features per 1m bar
- **Cross-Validation**: D1+D2+D3 fusion = 73% accuracy for 15m sweeps

## 🤖 AI Agent Quick Start

### Find Stealth Patterns
```python
# Load 1-minute data with syn_vol
df = pd.read_parquet('gold/canonical_1m/v1.1/date=2025-07-23/1m_2025-07-23.parquet')
stealth_events = df[df['syn_vol'] <= 0.0493]
```

### Cross-Dimensional Analysis
```python
# Load fusion results
stealth_fusion = pd.read_parquet('artifacts/irondisc/fusion/stealth_accumulation/production_stealth_patterns_2025-07-23_2025-08-07.parquet')
```

### Pattern Discovery
```python
# Load DTW clustering results
with open('artifacts/irondisc/dimensions/d1/dtw_clusters.json') as f:
    clusters = json.load(f)
```

## ⚠️ Important Notes

- **syn_vol Location**: Available in `gold/canonical_1m/v1.1/` files, NOT in basic samples
- **Timezone**: All timestamps in America/New_York (market timezone)
- **No PII**: Market data only, fully anonymized
- **Feature Engineering**: Sophisticated IRONCORE-derived features
- **Pattern Validation**: Statistical significance testing included

---

*Last Updated: September 15, 2025*
*This index enables AI agents to efficiently locate and analyze IRON pattern discovery datasets*