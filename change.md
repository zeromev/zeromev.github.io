# change log

The following improvements have been made to the MEV calculations. Numbers published before these date may differ from current values:

| date          | change                                                                      |
|---------------|-----------------------------------------------------------------------------|
|24 Feb 2023|_exchange rate improvements_<br><br>Usd amounts are now recalculated using base currencies where possible for greater accuracy of swaps and sandwiches.<br><br>Base currencies are currently considered to be: WETH, USDC, Dai and Tether.|
|24 Feb 2023|_improved unknown token handling_<br><br>Sandwiches are now calculated even for unknown tokens (those not available through the ethplorer.io), as long as the input and output token of the sandwich is known.|
