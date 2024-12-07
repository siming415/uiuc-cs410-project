# Netflix Reviews Analysis Project Documentation

## 1. Project Overview

### 1.1 Introduction & Motivation
This project addresses the challenge of analyzing large-scale user feedback for the Netflix mobile application. With over 118,000 reviews, manual analysis becomes impractical, necessitating an automated approach. We developed a system that combines information retrieval with sentiment analysis to extract meaningful insights from user reviews.

The choice of this approach was driven by two key observations:
1. The need to quickly identify and retrieve specific types of feedback (search functionality)
2. The importance of understanding overall user sentiment patterns (sentiment analysis)

### 1.2 Methodology Selection
We chose a hybrid approach combining BM25 search with machine learning-based sentiment analysis for several reasons:

#### BM25 Search Selection:
- Superior handling of term frequency saturation compared to TF-IDF
- Better performance with varying document lengths
- Proven effectiveness in production search systems
- Lower computational overhead compared to neural search methods

#### Machine Learning Models Selection:
Logistic Regression as primary model due to:
- Interpretability of results
- Efficient training on large datasets
- Good performance with high-dimensional text data
- Probability outputs for confidence measurement

## 2. Data Processing Pipeline

### 2.1 Text Preprocessing Strategy
Our preprocessing pipeline was carefully designed to balance information preservation with noise reduction:

#### Tokenization Choice:
We selected TreebankWordTokenizer over simpler alternatives because:
- Better handling of contractions (crucial for sentiment analysis)
- Proper treatment of punctuation marks
- Consistent handling of special characters
- Superior performance with informal language common in reviews

#### Stop Words Management:
The decision to retain negation words while removing other stop words was based on:
- Impact analysis showing 15% improvement in sentiment accuracy
- Preservation of critical sentiment indicators (e.g., "not good", "no issues")
- Reduction in false positive classifications

### 2.2 Feature Engineering Decisions
The TF-IDF vectorization with 5000 features was chosen based on:
- Vocabulary coverage analysis showing 95% content representation
- Memory usage optimization
- Processing speed requirements
- Empirical performance testing across different feature sizes

## 3. Search Implementation

### 3.1 BM25 Algorithm Configuration
Our BM25 implementation uses optimized parameters:
- k1 = 1.5: Chosen through empirical testing showing best performance for review-length documents
- b = 1.0: Full document length normalization to handle varying review lengths

The parameter selection was based on:
- Cross-validation across different query types
- Performance metrics (NDCG, Precision)
- Response time requirements

### 3.2 Query Processing
The query processing pipeline includes:
- Term normalization
- Stop word filtering (with negation preservation)
- Query expansion for common app-related terms

## 4. Sentiment Analysis System

### 4.1 Model Architecture Decisions
The multi-model approach was chosen to provide robust results:

#### Logistic Regression (Primary Model):
- Achieved 80% accuracy with balanced performance across classes
- Provides interpretable feature importance
- Efficient training and prediction times
- Well-suited for text classification tasks

#### Support Vector Machine (Secondary Model):
- Comparable accuracy to Logistic Regression
- Better handling of non-linear patterns
- More computationally intensive but useful for verification

### 4.2 Performance Analysis
Detailed analysis of model performance reveals:
- Strong performance on extreme sentiments (positive/negative)
- Challenge with neutral class classification (common in sentiment analysis)
- Consistent performance across different app versions

## 5. How to Use the Software

### 5.1 Prerequisites
1. Prepare your Netflix reviews dataset in CSV format
2. Install required Python packages:
   - pandas, numpy, nltk, scikit-learn
   - whoosh for search functionality
   - seaborn, matplotlib for visualizations

### 5.2 Basic Usage
1. Load and process your data
2. Use search functionality to find relevant reviews
3. Apply sentiment analysis to understand user feedback
4. Generate visualizations and reports

### 5.3 Advanced Features
- Custom search queries
- Batch sentiment analysis
- Performance metrics generation
- Trend analysis across versions

## 6. Results and Impact

### 6.1 Search Performance
- NDCG@10: 1.0000
- Precision@10: 1.0000
- Average query time: <100ms

### 6.2 Sentiment Analysis Results
Distribution of sentiments:
- Negative: 48.62% (57,537 reviews)
- Positive: 41.00% (48,518 reviews)
- Neutral: 10.38% (12,278 reviews)

### 6.3 Key Insights
1. Most common issues identified:
   - App stability
   - Streaming quality
   - Login problems

2. Version-specific patterns:
   - Impact of updates on user satisfaction
   - Feature reception across versions
   - Bug report frequencies

## 7. Future Improvements

### 7.1 Planned Enhancements
1. Implementation of deep learning models
2. Multi-language support
3. Real-time processing capabilities
4. Enhanced visualization tools

### 7.2 Scalability Considerations
- Database integration for larger datasets
- Distributed processing capabilities
- API development for broader access
