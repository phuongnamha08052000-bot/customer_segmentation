# customer_segmentation
Conduct unsupervised learning to segment customers based on their behavioral data
Project Overview
Unsupervised customer segmentation on a direct-marketing dataset to uncover behavioral segments that differ on spend mix, channel usage, recency, and promotion responsiveness. The workflow covers data cleaning, outlier handling, feature engineering, scaling, dimensionality reduction for visualization, and a model bake-off across several clustering algorithms. 

Data & Features 
Core behavior & spend: Mnt* (wines, meat, fish, fruits, sweets, gold), Num*Purchases (web, catalog, store, deals), NumWebVisitsMonth, Recency, Response/AcceptedCmp*
Light cleaning: consolidated rare categories, imputed Income median, capped one extreme outlier, dropped ID.
Derived examples used in profiling / rules: Expenses (aggregate spend), NumTotalPurchases, AmountPerPurchase, TotalAcceptedCmp.

Method
1. Preprocess: numeric scaling with z-scores; minimal category consolidation; outlier cap for Income.
2. Dimensionality reduction: PCA for plotting/structure checks (clustering run on standardized original features).
3. Model suite:
K-Means (k=3…6) with elbow/silhouette sweeps
Hierarchical (Ward) with dendrogram inspection, final k=3
DBSCAN density check (used mainly to validate structure)
GMM, K-Medoids (additional comparisons)
4. Evaluation: Silhouette (↑), Calinski-Harabasz (↑), Davis-Bouldin (↓) on the chosen labels; z-score cluster profiles (mean z per feature per segment); Kruskal-Wallis tests to flag features that differ significantly across clusters; surrogate decision tree to extract human-readable rules.

Model Comparison 
K-Means (k=3)
Silhouette = 0.3752, CH = 2401.84, DB = 1.1043 → best overall separation/compactness among tested options.
Z-score profiles were clean and consistent with the tree rules (below).
Hierarchical Ward (k=3)
Silhouette = 0.2990, CH = 1720.37, DB = 1.2399 → stable, interpretable segments, but slightly weaker separation vs. K-Means.
DBSCAN / GMM / K-Medoids
Useful for triangulation (DBSCAN revealed dense cores + noise; GMM comparable but not superior on metrics here). Final selection favors K-Means (k=3) on objective metrics and clarity of profiles.
