# Loyalty_Program-Analytics-PowerBI_Dashboard
Interactive Power BI dashboard delivering insights into customer segmentation, flight activity, and promotion effectiveness in an airline loyalty-program

# Airline Loyalty Program Analytics 
# Abstract 

Customer loyalty programs play a central role in the airline industry, since maintaining long-term relationships 
with travelers can significantly influence the airline’s revenue stability and its advantage against its competitors. 
This project offers a detailed analysis of an airline loyalty program using Microsoft Power BI. The goal is to analyze 
customer behavior, evaluate enrollment numbers, assess how well a specific promotional campaign worked and 
identify any existing patterns in customer engagement. 
The analysis includes data regarding customer flight activity, loyalty program information, enrollment and 
cancellation records, customer lifetime value (CLV) etc. A multi-page interactive dashboard was created by using 
Power BI’s data modeling capabilities and DAX measures, to visualize key performance indicators (KPIs) and 
behavioral trends. 

The dashboard consists of five pages: Executive Summary, Customer Overview, Geographic Distribution, Flight 
Analysis, and Promotion Assessment. Each page focuses on a different dimension of the loyalty program. The 
Executive Summary page shows the key insights. The Customer Overview page presents a high-level 
segmentation of the customer base, highlighting active members, value distribution, and demographic 
characteristics. The Geographic Distribution page examines any regional variations in the customers’ activity and 
the associated value that they can bring. The Flight Analysis page focuses on travel behavior, lifecycle 
engagement patterns, and how promotional enrollments contribute to flight activity. The Promotion Assessment 
page ultimately assesses a specific promotional campaign’s efficacy by contrasting pre and post promotion 
periods across various metrics including enrollments, flight redemption percentage, churn rate, and customer 
lifetime value. 

This analysis demonstrated that the promotion significantly increased member enrollments while simultaneously 
maintaining overall customer quality and enhancing retention rates. Despite the fact that the promotion tended 
to attract customers with slightly lower value on average, the difference in CLV was small, implying that the 
campaign effectively broadened the loyalty program’s reach without jeopardizing its long-term profitability. 
Consequently, the project exemplifies how business intelligence tools can convert intricate airline loyalty data 
into practical insights that facilitate strategic decision-making for such organizations. 

# Section 1. Introduction 
In today’s competitive airline industry, loyalty programs are seen as essential tools for retaining customers and 
generating long-term revenue. With numerous options available to travelers, factors such as price, convenience, 
and loyalty incentives heavily influence their choices. This has led airlines to invest significantly in programs 
which are designed to reward their frequent travelers and encourage repeat business. 

A well-executed loyalty program enables airlines to gather extensive amounts of behavioral data, which can be 
then used to understand how customers interact with the brand, how frequently they travel, and how valuable 
they are over time. Analyzing this information can help with identifying which are the high-value customers and 
can further lead to the evaluation of marketing initiatives and optimization of the program’s overall performance. 
Customer Lifetime Value (CLV) is a very critical metric in loyalty program analytics, as it quantifies the total value 
a customer brings to the company throughout their relationship with the business. In the context of the airline 
sector, CLV takes into account factors such as frequency of travel, loyalty program participation, and redemption 
behavior. 

Another important aspect of loyalty programs is promotional campaigns. Airlines frequently run promotions 
aimed at increasing enrollment numbers and encouraging additional travel activity.  
The goal of this project is to analyze a dataset from an airline loyalty program and develop an interactive Power BI 
dashboard that will offer insights into customer segmentation, geographic distribution, travel behavior and 
effectiveness of the promotion campaign. 

# Business Questions and Analysis Focus: 
The dashboard provides an overview of enrollment performance and promotional activity, enabling users to 
monitor key metrics, track trends over time and evaluate the effectiveness of the campaigns of the airline. It 
answers these main questions: 

1. Who are the airline’s loyalty program members and how are they segmented? 
2. How do customers behave in terms of travel activity and program engagement? 
3. Did the promotional campaign successfully improve enrollment and loyalty program participation?

To answer these questions, a structured data model and a series of analytical visualizations were developed in 
Power BI.

# Section 2. Data Overview 
This project uses customer loyalty program data from Northern Lights Air, a fictitious Canadian airline. To 
improve program enrollment, the airline ran a promotion between February to April 2018. This dataset includes 
loyalty program enrollment and cancellation details, and additional customer information. 
More specifically the dataset contains the following CSV files: 

• Calendar.csv: contains Date, Start of Year, Start of Quarter and Start of Month columns 
• Customer Flight Activity.csv: contains Loyalty Number, Year, Month, Total Flights, Distance, Points 
Accumulated, Points Redeemed, Dollar Cost Points Redeemed columns 
• Customer Loyalty History.csv: contains Loyalty Number, Country, Province, City, Postal Code, Gender, 
Education, Salary, Marital Status, Loyalty Card, CLV, Enrollment Type, Enrollment Year, Enrollment Month, 
Cancellation Year, Cancellation Month columns 

# Section 3. Methodology:
# 3.1 Data Modeling 
The analysis was built using a structured data model consisting of (one fact and two dimension tables) both fact 
and dimension tables, as well as a complementary measure table, a period table and a customer advanced 
insights table. The central fact table contains flight activity data, while dimension tables provide descriptive 
information about customers and dates. 

The key tables used in the model include: 
Fact_FlightActivity 
This table contains information about customer flight activity and loyalty point usage, such as Loyalty Number, 
Months Since Enrollment, Points Redeemed, Total Flights etc. 
Dim_Customer 
This table contains customer-level information including the customer’s Loyalty Card tier, Education level, 
Gender, Marital Status, Enrollment Month Start, Cancellation Month Start, and CLV which indicates the 
Customer’s Lifetime Value. 
Dim_Date 
This table is utilized as a calendar table that is primarily used to enable time-based analysis and filtering across 
the dataset. 

# Relationships between tables: 
Relationships between these tables were implemented using a star schema structure.  
More specifically, the Dim_Customer and Dim_Date tables are connected using the following relationships: 

• The Enrollment Month Start column from the table Dim_Customer is connected to the Date column of the 
Dim_Date table using a Many to 1(*:1) Cardinality and Single Cross-filter direction. 
• The Cancellation Month Start column from the table Dim_Customer is connected to the Date column of 
the Dim_Date table using a Many to 1(*:1) Cardinality and Single Cross-filter direction. 
Additionally, Fact_FlightActivity and Dim_Date tables are connected using the relationship: 
• The Activity Month Start column from the table Fact_FlightActivity is connected to the Date column of the 
Dim_Date table using a Many to 1(*:1) Cardinality, with direction set as Single Cross-filter and the 
relationship is set as an active relationship. 
Also, Fact_FlightActivity and Dim_Customer tables are connected using the relationship: 
• The Loyalty Number column from the table Fact_FlightActivity is connected to the Loyalty Number column 
of the Dim_Customer table, which is their common key, using a Many to 1(*:1) Cardinality, with direction 
set as Single Cross-filter and the relationship is set as an active relationship. 
This modeling approach allowed to efficiently aggregate the data while also enabling flexible filtering by customer 
attributes and specific time periods. 

# 3.2 Key Measures 

To support the analysis a range of DAX measures have been developed. 
One of the most crucial measures is Active Members, which identifies the specific loyalty members who were 
active during a selected period of time. A member is considered active only if they have flight activity or loyalty 
point transactions (such as Accumulation of points, Redemption of points, or Redemption of Dollar cost points) 
within the period that has been specified and if their enrollment status is valid. More specifically, this measure is 
calculated by filtering customers who have activity within the selected date range and have not cancelled their 
membership before the selected period and additionally, these customers should have either flown, 
accumulated points, or redeemed points during this period. 

Another important measure for this analysis is Flights per Active Member, which measures the customer’s 
engagement by dividing total flights by the number of active members and counting only distinct flight activities. 
One such measure is created per Month and one per Year, to be used for the broader time analysis of flights of 
each active member. 

Customer Lifetime Value (CLV) is also extensively used in this analysis to quantify the economic worth that a 
customer contributes to the airline throughout their engagement with this organization. Within this framework, 
CLV functions as a crucial metric for assessing customer profitability, facilitating the categorization of customers 
into distinct value bands. Consequently, this segmentation enables the dashboard to pinpoint which groups of 
customers add the most economic benefit to the loyalty program. 

Furthermore, the revenue within the loyalty program is estimated using the metric Dollar Cost Points 
Redeemed, which represents the monetary value of loyalty points redeemed for flights. Specifically, in this 
analysis, this is used as a representative of customer spending within the airline loyalty system. 
Furthermore, some additional measures were created and are specifically utilized to evaluate the promotional 
campaign. 
These measures compared the performance metrics between the two specified time periods: the pre
promotion period (November 2017 to January 2018) and the promotion period (February 2018 to April 2018). 
The definition of these set time periods inside the DAX calculations, allow the dashboard to show a more 
straightforward distinction of the two periods without the user having to filter them manually. 
For instance, Average Monthly Enrollment during the Promotion (Promo) and before the promotion (PrePromo) 
is used to show the number of enrollments (per month) for comparison (before and during the months of 
February and April 2018 when the promotion was ran). 
This is intended to show the average number of new 
members joining the loyalty program each month during the specific period. This comparison between the 
average monthly enrollment during the promotional period and the enrollment rate before the promotion, makes 
it easier to discern if the campaign was successful at attracting new customers. The significant increase that was 
observed in this metric points out that the campaign managed to increase customer interest, while 
simultaneously encouraging new members to join the program. 

Churn Rate represents the proportion of loyalty members who cancel their membership or become inactive 
within teh specified time frame. It is very important for understanding if a program is sustainable. Churn is 
essential for loyalty program management because attracting new members is only beneficial if those members 
remain engaged over time and customer acquisition alone does not guarantee success and therefore, a high turn 
rate could be used as an indicator of dissatisfaction. This analysis suggests that the promotional campaign not 
only increased enrollments, but also reduced churn as seen by the lower churn rates during and after the 
promotion. This indicates that the new members were more likely to stay in the loyalty program, which is 
beneficial for the airline’s long-term success, rather than leaving soon after joining.  

Redemption Value provides insight into how actively members use their loyalty points in the program. In airline 
loyalty programs, customers earn points through flying and can later use these points and redeem them directly 
for flights, upgrades, or other rewards. The program gives points a monetary value when the points are redeemed, 
and this value is noted as the Dollar Cost Points Redeemed. Because redemption value indicates the economic 
value of benefits received by members, it is used in this research as an indicator of the revenue generated in the 
loyalty system. The rise in redemption value throughout the promotion time demonstrates that customers are 
actively using the rewards system and are more engaged with the loyalty program.  

Furthermore, to ascertain the contribution of the promotional campaign's clients to the airline's flight activity, the 
Percentage of Flights from Promotion Members was calculated. This metric provides a comparative analysis of 
the total flight activity of all active members against the flight activity of those who participated in the promotion. 
By checking this percentage, it becomes possible to evaluate the extent to which newly acquired clients are 
influencing overall travel patterns. The considerable share of flights attributed to promotional members indicates 
that the campaign successfully attracted passengers who actively engage with the airline, rather than merely 
registering without generating substantial value. 

Additionally, directional arrows were used in the dashboard to visually show if a metric increased or decreased 
during the promotion.   

In general, the use of DAX measures enables the dashboard to carry out intricate, dynamic calculations based on 
user-defined filters like enrollment year or loyalty card tier. This adaptability not only supports more profound 
data investigation but also ensures the accurate representation of underlying relationships within the 
visualizations. As a consequence, this integration of metrics, calculated measures, and temporal comparisons 
shows a robust analytical framework for evaluating the efficacy of the airline's rewards program. 

# Section 4. Dashboard Structure 

The final Power BI dashboard consists of five pages designed to guide the user through different layers of the 
analysis. 

The pages include: 
1. Home Page 
2. Executive Summary 
3. Customer Overview 
4. Geographic Distribution 
5. Flight Analysis 
6. Promotion Assessment 
Each page presents a set of visualizations that highlight different aspects of the loyalty program.

# Section 5. Conclusion 

This case study highlights the power of data analytics in the aviation sector. It shows how intricate loyalty 
program datasets can be transformed into high level business intelligence, ultimately uncovering the trends that 
matter most for growth and retention. By analyzing geographic trends and travel patterns throughout this 
dashboard, we can see the direct impact of the 2018 promotion. The analysis confirms that the campaign 
effectively scaled the loyalty program and boosted activity levels, all while maintaining a consistent standard for 
new members. Also, the results show that while customer value stayed steady, retention actually improved. The 
promotion proved to be a versatile tool for acquisition, successfully attracting new members from all tiers, 
including the top participants. The results indicate that the promotional initiative successfully broadened the 
loyalty program's reach while simultaneously preserving its enduring value. Ultimately, this project underscores 
the significance of data-informed decision-making in the administration of loyalty programs. Moreover, by 
integrating customer segmentation, behavioral analysis, and promotional performance assessment, airlines can 
gain a more comprehensive understanding of their clientele and formulate strategies that optimize long-term 
profitability. 

# Resources: 
Dataset link: https://mavenanalytics.io/data-playground/airline-loyalty-program
