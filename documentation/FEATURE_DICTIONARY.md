# IRON Feature Dictionary

## 🎯 Core Trading Features

### D1 Liquidity Dimension
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `syn_vol` | Synthetic volume ratio | 0.0-5.0+ | ≤0.0493 = stealth activity |
| `liq_ratio` | Liquidity concentration | 0.0-1.0 | Higher = more concentrated |
| `dtw_cluster` | DTW cluster assignment | 0-N | Behavioral regime classification |
| `hmm_state` | Hidden Markov state | 0-4 | Microstructure state |

### D2 ICT Macro Dimension
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `pll_strength` | Price level liquidity | 0.0-1.0 | Strength of price level |
| `macro_phase` | ICT macro phase | 1-4 | Market cycle position |
| `cycle_position` | Cycle timing | 0.0-1.0 | Position in cycle |
| `spooling_score` | Accumulation/distribution | -1.0-1.0 | Directional bias |

### D3 FPFVG Dimension
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `fvg_score` | Fair value gap strength | 0.0-1.0 | Gap significance |
| `fvg_direction` | Gap bias | -1,0,1 | Bearish/Neutral/Bullish |
| `motif_match` | Sequence pattern match | 0.0-1.0 | Pattern confidence |
| `survival_prob` | Gap fill probability | 0.0-1.0 | Likelihood of fill |

### D4 News Context
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `news_impact` | Event impact score | 0.0-1.0 | Significance of news |
| `event_proximity` | Time to/from event | -N-+N mins | Distance from news |
| `correlation_strength` | News-price correlation | 0.0-1.0 | Reaction strength |

### D5 Weekly Profiles
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `dow_regime` | Day-of-week cluster | 0-6 | Weekly behavioral pattern |
| `weekly_position` | Week cycle position | 0.0-1.0 | Position in week |
| `seasonal_bias` | Historical bias | -1.0-1.0 | Directional tendency |

### D6 Sequential Dependencies
| Feature | Description | Range | Interpretation |
|---------|-------------|-------|----------------|
| `sequence_id` | Pattern sequence ID | String | Sequence identifier |
| `causal_strength` | PC algorithm strength | 0.0-1.0 | Causal relationship |
| `temporal_lag` | Event lag (minutes) | 1-60 | Time dependency |

## 🎯 Target Labels (What We're Predicting)

### Liquidity Sweep Events
| Label | Description | Binary | Timeframe |
|-------|-------------|--------|-----------|
| `sweep_pdh_15m` | Previous Day High sweep | 0/1 | Next 15 minutes |
| `sweep_pdl_15m` | Previous Day Low sweep | 0/1 | Next 15 minutes |
| `sweep_pdh_30m` | Previous Day High sweep | 0/1 | Next 30 minutes |
| `sweep_pdl_30m` | Previous Day Low sweep | 0/1 | Next 30 minutes |
| `sweep_pdh_60m` | Previous Day High sweep | 0/1 | Next 60 minutes |
| `sweep_pdl_60m` | Previous Day Low sweep | 0/1 | Next 60 minutes |

## 📊 Base Market Data

### OHLCV Features
| Feature | Description | Units |
|---------|-------------|-------|
| `open` | Opening price | Points |
| `high` | High price | Points |
| `low` | Low price | Points |
| `close` | Closing price | Points |
| `volume` | Volume traded | Contracts |
| `ts` | Timestamp | UTC datetime |

### Derived Price Features
| Feature | Description | Calculation |
|---------|-------------|-------------|
| `price_relativity` | Multi-timeframe position | (close - level) / ATR |
| `range_pct` | Bar range percentage | (high - low) / close |
| `wick_ratio` | Wick to body ratio | wick_size / body_size |

## 🔍 Pattern Recognition Features

### Statistical Features
- **Moving averages**: 5,10,20,50,200 period EMAs
- **Volatility**: ATR, Bollinger Band position
- **Momentum**: RSI, MACD, Rate of Change
- **Volume**: VWAP deviation, volume profile

### Microstructure Features
- **Imbalance ratios**: Bid/ask dynamics
- **Tick analysis**: Price movement patterns
- **Time-based**: Session time, market hours
- **Structural levels**: Support/resistance strength

## 🎲 Usage Examples

### Stealth Detection Pattern
```python
# High probability stealth accumulation
stealth_setup = (
    (data['syn_vol'] <= 0.0493) &           # Low synthetic volume
    (data['pll_strength'] > 0.7) &          # Strong price level
    (data['fvg_score'] > 0.5) &             # Active fair value gap
    (data['hmm_state'] == 2)                # Accumulation state
)
```

### Weekly Regime Analysis
```python
# Monday morning behavior vs Friday afternoon
monday_am = data[(data['dow_regime'] == 0) & (data['session_hour'] < 12)]
friday_pm = data[(data['dow_regime'] == 4) & (data['session_hour'] > 14)]
```

---

*This feature dictionary enables AI agents to understand the sophisticated market microstructure patterns that IRONDISC algorithms are designed to detect.*