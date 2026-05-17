🛠 Feature Scaling: Comparative Analysis
To ensure the K-Means clustering algorithm performs optimally, multiple data transformation techniques are evaluated. Since distance-based algorithms are sensitive to feature scales, selecting the right transformer is critical for meaningful playlist generation.

🧪 Scalers Evaluated
Benchmarking of the following transformers to observe their impact on the Spotify audio features:

MinMaxScaler: Rescales data to a fixed [0,1] range.

Observation: Best for preserving the original distribution while aligning outliers like tempo and loudness with Spotify's native 0–1 metrics.

StandardScaler: Standardizes features to a mean of 0 and a standard deviation of 1.

Observation: Useful for features following a Normal distribution, but less intuitive for visualization (e.g., Radar Charts).

RobustScaler: Uses the Interquartile Range (IQR) for scaling.

Observation: Effectively handled potential outliers in features like instrumentalness without compressing the majority of the data.

📊 Comparative Rationale
After testing, MinMaxScaler was selected as the primary transformer for this prototype.

Feature	Pre-Scaling Range	Post-Scaling (MinMax)
Tempo	60 – 200 BPM	0.0 – 1.0
Loudness	-60 – 0 dB	0.0 – 1.0
Danceability	0.0 – 1.0	0.0 – 1.0
Conclusion: MinMaxScaler provided the best balance between mathematical neutrality and interpretability for the Moosic business stakeholders. It ensures that no single feature dominates the clustering process due to its raw magnitude.

💻 Implementation
Python
from sklearn.preprocessing import MinMaxScaler, StandardScaler, RobustScaler

# Comparative fitting (MinMaxScaler selected)
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(df[audio_features])
