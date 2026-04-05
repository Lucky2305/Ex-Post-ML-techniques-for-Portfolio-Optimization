# Portfolio Optimization with Regularization
This project explores robust portfolio optimization techniques using real-world equity data from the Indian stock market (NSE). It demonstrates how statistical and structural regularization improve stability compared to classical Markowitz optimization.

## Methods Implemented
### Ledoit-Wolf Shrinkage (Statistical Regularization)
Addresses instability in covariance estimation

Improves conditioning of covariance matrix

Compared against:

Sample covariance (Markowitz)

Key steps:

Compute sample covariance matrix

Calculate condition number

Apply Ledoit-Wolf shrinkage

Optimize for Maximum Sharpe Ratio

 ###Hierarchical Risk Parity (HRP)
Uses clustering to model risk structure

Avoids matrix inversion

Steps:

Distance matrix from correlations

Hierarchical clustering (dendrogram)

Recursive bisection allocation


# Bootstrap Stability Analysis: Sample vs Shrunk Covariance
<img width="857" height="555" alt="Screenshot 2026-04-05 at 10 29 50 PM" src="https://github.com/user-attachments/assets/51c2e2b1-97b1-42f3-92a8-5cffd373718b" />

This figure compares the stability of the sample covariance matrix and the Ledoit-Wolf shrinkage estimator using bootstrap resampling. The distribution of condition numbers for the sample covariance matrix is widely dispersed and highly right-skewed, with values ranging from around 50 to over 600, indicating that it is frequently ill-conditioned and sensitive to small changes in the data. Such instability can lead to unreliable matrix inversion and highly erratic portfolio weights in optimization. In contrast, the shrunk covariance matrix exhibits a much tighter and more concentrated distribution, with condition numbers largely confined to a narrow range between approximately 20 and 60. This demonstrates significantly improved numerical stability and robustness across different samples. The results clearly show that shrinkage effectively regularizes the covariance estimation by reducing noise and controlling extreme eigenvalues, thereby producing more stable and reliable inputs for portfolio optimization.
# Covariance Matrix Comparison: Sample vs Ledoit-Wolf Shrinkage
<img width="1289" height="556" alt="Screenshot 2026-04-05 at 10 32 12 PM" src="https://github.com/user-attachments/assets/b2e910f6-bc68-4c5c-89b6-0801c5adf62f" />

This figure presents a side-by-side heatmap comparison of the sample covariance matrix and the Ledoit-Wolf shrunk covariance matrix for the selected NSE stocks. The sample covariance matrix exhibits more pronounced variability, with several extreme values and sharper contrasts across entries, indicating the presence of noise and estimation error inherent in finite samples. These fluctuations can distort the true underlying relationships between assets and lead to unstable portfolio optimization outcomes. In contrast, the shrunk covariance matrix appears smoother and more structured, with reduced intensity in extreme values and more consistent patterns across the matrix. This reflects the effect of shrinkage, which pulls the sample estimates toward a more stable target, thereby reducing noise and improving numerical conditioning. Overall, the visualization highlights how Ledoit-Wolf shrinkage produces a more reliable and robust estimate of asset covariances, making it better suited for practical portfolio construction.

# Hierarchical Clustering Structure: HRP Dendrogram
<img width="1389" height="790" alt="Unknown" src="https://github.com/user-attachments/assets/c1cdc781-c78d-4400-b66e-ebb1004a9932" />

This dendrogram illustrates the hierarchical clustering structure of the selected NSE stocks based on their return correlations, forming the foundation of the Hierarchical Risk Parity (HRP) portfolio construction. The clustering reveals distinct groupings of stocks that share similar risk characteristics, as assets that are more highly correlated are merged at lower linkage distances. For instance, metal sector stocks such as HINDALCO.NS, JINDALSTEL.NS, and TATASTEEL.NS are clustered closely together, indicating strong co-movement. Similarly, IT stocks like TCS.NS, INFY.NS, and HCLTECH.NS form another coherent cluster, while banking stocks including HDFCBANK.NS, ICICIBANK.NS, and KOTAKBANK.NS are grouped together, reflecting shared exposure to financial sector dynamics. Consumer-oriented stocks such as HINDUNILVR.NS, NESTLEIND.NS, and ITC.NS also exhibit clustering behavior, albeit with slightly more dispersion.

The hierarchical structure ensures that diversification is achieved across these clusters rather than within highly correlated groups. By recursively splitting the dendrogram and allocating weights based on cluster-level risk, HRP avoids over-concentration in similar assets and produces a more balanced and robust portfolio. This data-driven clustering approach highlights how HRP captures the underlying topology of asset correlations, making it a powerful alternative to traditional mean-variance optimization.

# Portfolio Allocation Comparison: MPT vs HRP
<img width="998" height="649" alt="Screenshot 2026-04-05 at 10 35 04 PM" src="https://github.com/user-attachments/assets/8a268835-2e45-4d21-bea8-fb9ec6b68624" />

This figure compares the portfolio weights assigned by the traditional Mean-Variance Optimization (MPT) framework and the Hierarchical Risk Parity (HRP) approach across the selected NSE stocks. The MPT portfolio exhibits highly concentrated and unstable allocations, with extreme positive and negative weights, including significant short positions in certain assets and disproportionately large exposures to others. This behavior is a direct consequence of the sensitivity of MPT to estimation errors in the covariance matrix, which often leads to overfitting and unintuitive allocations.

In contrast, the HRP portfolio produces more balanced and diversified weights, with all allocations remaining positive and more evenly distributed across assets. By leveraging hierarchical clustering and recursive risk allocation, HRP avoids excessive concentration in any single asset or cluster and instead spreads risk more uniformly. This results in a more stable and interpretable portfolio that is better aligned with practical investment constraints, such as long-only positions and reduced turnover. Overall, the comparison highlights how HRP provides a robust alternative to classical optimization by mitigating the impact of estimation noise and promoting diversification.

# Banking Sector Weight Sensitivity During COVID-19 Crisis
<img width="995" height="534" alt="Screenshot 2026-04-05 at 10 36 50 PM" src="https://github.com/user-attachments/assets/9129a118-28d0-4a5f-9b96-6c9d9343e7f5" />

This figure illustrates the evolution of portfolio weights assigned to key banking stocks—ICICIBANK.NS, HDFCBANK.NS, and KOTAKBANK.NS—under both Mean-Variance Optimization (MPT) and Hierarchical Risk Parity (HRP) during the COVID-19 crisis period. The MPT-based allocations display extreme volatility, particularly for ICICIBANK.NS, where the weight sharply drops to highly negative levels before reverting back toward neutral. Similar instability, though less severe, is observed for KOTAKBANK.NS. This behavior reflects the sensitivity of MPT to sudden changes in covariance estimates during periods of market stress, leading to large and often impractical short positions.

In contrast, the HRP allocations remain remarkably stable throughout the same period, with only minor fluctuations and consistently positive weights. By relying on hierarchical clustering and risk-based allocation rather than direct covariance inversion, HRP is less affected by short-term market shocks and estimation noise. As a result, it produces more resilient and interpretable portfolio allocations, even during periods of heightened uncertainty. This comparison highlights the superior robustness of HRP in managing portfolio weights under crisis conditions, making it more suitable for real-world investment applications.

# Conclusion

This study highlights the critical importance of regularization in practical portfolio optimization. The results clearly demonstrate that traditional Mean-Variance Optimization (MPT), when combined with the sample covariance matrix, is highly sensitive to estimation errors, leading to unstable weights, extreme allocations, and poor robustness—especially during periods of market stress. The bootstrap analysis further confirms that the sample covariance matrix is ill-conditioned and unreliable across different data samples.

In contrast, both forms of regularization significantly improve stability. The Ledoit-Wolf shrinkage estimator enhances the conditioning of the covariance matrix, reducing noise and producing more consistent portfolio weights. Meanwhile, Hierarchical Risk Parity (HRP) offers a structurally robust alternative by leveraging clustering to allocate risk more effectively, resulting in diversified, stable, and interpretable portfolios with lower turnover.

Overall, the findings reinforce that regularization—both statistical and structural—is not optional but essential for real-world quantitative portfolio management, as it ensures stability, robustness, and better out-of-sample performance.

