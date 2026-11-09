# MSCS 634 – Lab 6: Association Rule Mining with Apriori and FP-Growth

**Name:** Umama Azhar
**Course:** MSCS 634 – Advanced Big Data and Data Mining

## Purpose
This lab applies association rule mining to retail transaction data to find products that customers tend to buy together. I used the Apriori and FP-Growth algorithms to find frequent itemsets, generated association rules from them (support, confidence and lift), visualized the results with Seaborn, and compared the two algorithms.

## Dataset
Online Retail dataset (UCI Machine Learning Repository). After cleaning (removing cancelled orders, returns, rows with no product name, and non-product items such as postage and fees), I used the **France** subset: 382 baskets and 1,560 products.

## Files
- `Lab6.ipynb` – the full notebook with code, charts and written analysis for every step
- `README.md` – this summary

## Key Insights
- Both algorithms (minimum support 0.05) found the same **113 frequent itemsets** (76 single items, 34 pairs, 3 triples) and the same **38 rules** at a confidence threshold of 0.6.
- The strongest associations by lift are matched product sets: skull paper cups and plates (lift 13.9), children's cutlery Dolly Girl and Spaceboy (lift 12.6), and the Bakelike alarm clocks in different colours (lift 8 to 9).
- The most reliable rules come from the red spotty party set. Baskets with the napkins and plates or cups contain the third item 97.5% of the time, and the spotty plates lead to the spotty cups with 96% confidence.
- Every rule has a lift well above 1 (the lowest is about 3.5), so these are real associations and not just popular items appearing together.
- **Apriori was faster than FP-Growth on this dataset** (about 0.0215 s vs 0.0337 s, averaged over 20 runs). The dataset is small and the support threshold fairly high, so FP-Growth's tree-building cost outweighed its savings. FP-Growth is expected to win on larger data or lower thresholds, which I did not test.

## Challenges and Decisions
- **File path error:** the dataset was inside a folder that had the same name as the file (`data.csv`). I listed the folder's contents and used the full path to the file.
- **Postage dominated the results:** it appeared in about 300 of 392 baskets and would have created meaningless rules, so I removed it and other non-product rows.
- **Dataset size:** I used only the France subset so the algorithms run quickly.
- **Support threshold:** I chose 0.05, which gave a useful number of itemsets for a small dataset.
- **Timing:** a single run took only about 0.03 s, so I averaged 20 runs of each algorithm for a fairer comparison.

## How to Run
Install the libraries (`pip install pandas mlxtend seaborn matplotlib`), download the Online Retail dataset, update the file path in the notebook, and run all cells.
