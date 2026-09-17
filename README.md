Commit Message:

feat: Add SOL investment notifications with Phantom & FOMO charts

- Integrated alert system to notify the best times to buy and sell SOL.
- Implemented chart generation for market trends using Phantom wallet data.
- Added FOMO analysis to detect potential market spikes.
- Extended `analyze.py` to include real-time RSI, MACD, and volume triggers.
- Created notification logic in `send_sms.py` to deliver actionable alerts.
- Updated dashboard to visualize timing signals and performance indicators.

Affected Files:
src/analyze.py
src/send_sms.py
dashboard/
requirements.txt

New Features:
Real-time notifications for ideal SOL investment and selling timings.
Phantom-based chart visualization with FOMO detection.
Integrated alerting system to optimize trade decisions.

Next Steps:
Implement user-specific thresholds for alerts.
Add backtesting of FOMO triggers for predictive accuracy.
Expand notification channels beyond SMS.
