# YouTube-Data-Analysis-System

## 1.Introduction and Background:  
This project embarks on a dual mission to revolutionize the YouTube landscape.  

Firstly, it endeavors to create an intuitive and comprehensive dashboard designed to streamline the onboarding process for aspiring YouTube creators. The primary aim is to empower new creators to navigate their content creation journey effortlessly, optimizing both the quality of their content and revenue potential. This user-friendly environment seeks to foster a vibrant community of digital producers who can navigate YouTube's intricacies with ease, unlocking their creative potential.  

Simultaneously, the project addresses the strategic challenge of identifying trending content on YouTube by developing mechanisms to analyze emerging trends. This facilitates advertisers in strategically positioning their advertisements to reach the widest and most relevant audience, creating a symbiotic relationship that enhances the overall advertising experience on YouTube for both content creators and advertisers.

## 2. Objective:  
The objective of this project is to develop a system for analyzing YouTube data to answer two questions:  
* How does our project's dashboard simplify the process for new YouTube creators to begin their journey, enhancing their content and revenue, while fostering a successful community of digital producers?
* How can we identify trending content on YouTube to strategically position advertisements, ensuring advertisers reach the widest and most relevant audience?  
## 3. System Architecture:
### 3.1Project Flow Chart
<img width="800" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/93999e11-6a3e-439c-a78e-775ca42650b6">

We developed a pipeline to load unstructured YouTube Data into AWS S3, then harnessed AWS Data Wrangler based on Python for data wrangling. The refined data was subsequently loaded into Amazon Redshift by building AWS Glue pipeline, ensuring data integrity and readiness for advanced querying and analytics. AWS SageMaker and AWS Athena will be used for Machine Learning and Analysis. AWS QuickSight will be used for the Visualization.
### 3.2 About the dataset:
<img width="500" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/d9964924-590d-4443-9827-59f0e78ea64f">  

This dataset is from Kaggle, and it includes several months (and counting) of data on daily trending YouTube videos. Data is included for the IN, US, GB, DE, CA, FR, RU, BR, MX, KR, and JP regions (India, USA, Great Britain, Germany, Canada, France, Russia, Brazil, Mexico, South Korea, Japan), with up to 200 listed trending videos per day. The size of it is around 4GB and we will store all the data into the S3 bucket for normal usage.  
## 4. Methodology:
### 4.1 The ETL Process
For ETL process, we have opted for AWS Glue, a fully managed service that simplifies data extraction, transformation, and loading for analytics. AWS Glue streamlines the ETL process, allowing for automated data handling and creating a Glue data catalog. This catalog is pivotal for further analysis with AWS Athena (SQL) and data visualization using AWS Quicksight. Our initial step involves creating a Glue data catalog for datasets from different countries, available in CSV or JSON formats. Segregating data by country not only eases analysis but also organizes data management more effectively. We then establish an automated ETL pipeline to create a JOIN between cleaned JSON and CSV files. The reason to choose ETL pipeline over SQL is ease of use and there exists incompatibility of schemas between JSON and CSV formats, which using SQL for this task often leads to errors. The ETL pipeline can simplify this process and seamlessly integrate into the Glue data catalog, enabling us to leverage all AWS tools for comprehensive analysis.
 <img width="500" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/817dcd2b-e8be-455b-853d-b6662a3d7eef">

Our ETL process is further enhanced by AWS Lambda, where we use Lambda functions to trigger ETL jobs in response to new data arrivals or schedule times. By decoupling our ETL workload from any server, we ensure that the process is not only efficient but also available and scalable.
For data transformation, AWS Glue's dynamic frame concept allows us to handle semi-structured data and manage complex data types easily. Once the data is prepared, we use AWS Athena to run SQL queries directly against our data lake, extracting insights without the need for traditional data warehouse solutions.
### 4.2 Machine Learning Models:
This report presents a comprehensive analysis of YouTube data, employing Amazon SageMaker to streamline the development process. In the realm of model selection, SageMaker's versatility shines through, offering a range of pre-built algorithms and support for custom models to suit the unique characteristics of the data. Implementation details highlight the platform's seamless and scalable environment for model training, while hyperparameter tuning ensures optimal performance. Deployment becomes a straightforward task, thanks to SageMaker's features, allowing for the integration of trained models into production environments with auto-scaling and monitoring capabilities. The results reveal insightful trends, user behaviors, and content preferences within the vast YouTube landscape, highlighting the potency of combining data analysis with the robust capabilities of SageMaker.

### 4.3 Data Analysis and Insights:
Visualizations and dashboard were created in AWS QuickSight

 <img width="800" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/66ada0b8-0078-47cd-a83c-d0f189bc7725">
 
## 5.Results:
### 5.1 Understanding the relationship between likes and View
In our quest to unravel the intricacies of human engagement on YouTube, our analysis hones in on the dynamics of relationships and preferences, with a specific emphasis on likes. Aggregating global data, we have meticulously crafted a comprehensive correlation graph that illuminates patterns in viewer interactions, showcasing a robust positive correlation between likes and views. To refine our insights, we have initiated the removal of outliers, strategically filtering the data to concentrate on predominant trends and enhance clarity, aiming for a more representative understanding of typical viewer interactions across YouTube content.
<img width="500" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/1bcc4b2f-a25c-4551-ba01-a66ee9411850">

As we shift our focus to explore viewer engagement dynamics on a country-specific level, our analysis aims to uncover unique patterns and preferences within each distinct region. By examining the relationship between likes and views across various countries, we anticipate revealing valuable insights into how content resonates differently across cultural and geographical landscapes. Despite the diversity in regions, a consistent positive correlation between likes and views emerges, indicating a universal pattern of viewer engagement. To delve deeper into this phenomenon, our report will now narrow its focus to the data from the United States, offering a detailed exploration of viewer interactions and content reception within one of the largest YouTube markets.
 
### 5.2 Understand all aspect of the video
In our exploration of YouTube trends, we recognize that factors beyond likes, such as comments or dislikes, can also significantly influence a video's popularity. These elements collectively contribute to a video's ability to trend and captivate viewers. To gain a comprehensive understanding of these interrelationships and their impact on viewer behavior, we will create a heatmap. This heatmap will visually represent the correlations between different data points, such as views, likes, comments, and dislikes. By analyzing this correlation matrix, we can uncover which factors are most strongly associated with each other, thereby gaining deeper insights into the nuances of human engagement and interaction with YouTube content. This approach will provide a clearer picture of what drives viewership and how different aspects of a video contribute to its overall success on the platform.

<img width="500" alt="image" src="https://github.com/Traumia/YouTube-Data-Analysis-System/assets/57136475/bd49e812-8382-4fbe-a884-4a056380bd9b">

In the U.S., our analysis of YouTube trends underscores the paramount role of user engagement in determining a video's likelihood to trend. The highest correlation exists between the number of likes and view count, suggesting that likes act as a catalyst, initiating a cycle of increased visibility and viewer interaction that propels a video's popularity. This insight emphasizes the pivotal role of audience engagement, particularly through likes
A closer examination of popular YouTube channels reveals intriguing patterns, with MrBeast's widespread success attributed to a massive subscriber base. However, music-related content, especially in the KPOP genre, emerges as a dominant force among leading channels. Filtering the data by category reinforces this trend, positioning music, and particularly KPOP, at the forefront. This data presents a strategic opportunity for advertisers, indicating that placing advertisements within music videos, especially KPOP, can maximize exposure and engagement. By prioritizing music-related content over traditional categories like sports, advertisers stand to optimize their reach and impact on the platform, aligning their campaigns with the preferences and behaviors of the YouTube audience.

## 6. Discussion and Improvement:
Upon analyzing the YouTube data, we found several key trends regarding viewer engagement, content popularity, and effective monetization strategies. Our machine learning models, built and deployed using Amazon SageMaker, identified patterns that can predict video popularity, viewer retention rates, and potential advertisement success.

#### Recommendations for YouTube Creators:
Focus on creating content in trending niches as identified by our analysis.
Utilize SEO strategies for video titles and descriptions to improve discoverability.
Engage with the community to increase viewer retention and loyalty.

#### Recommendations for Advertisers:
Target advertisements on videos within trending categories to maximize reach.
Align ad placements with peak engagement times deduced from our analytics.
Collaborate with creators who have a high engagement rate for branded content.
Improvements in the future:
*	Use Data from various sources to make our training data more reliable
*	Implement a real-time data analytics pipeline to provide up-to-date insights for content creators and advertisers.
*	Experiment with advanced machine learning algorithms, including deep learning, to better understand and predict the nuances of user engagement.
