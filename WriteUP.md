# Logic Analysis of Various CHAT GPT Scripts
## Analysis of Causal Question: Discount Effect
The student uploaded a dataset relevant to a commercial chain that encodes:
- InvoiceNo: Invoice number (likely a unique identifier for each transaction)
- StockCode: Product/item code
- Description: Description of the product
- Quantity: The number of items purchased in the transaction
- InvoiceDate: Date and time of the invoice
- UnitPrice: Price per unit of the product
- CustomerID: Customer identifier
- Country: Country where the customer resides
This dataset has lots of different values which are predominately sorted by specific transactions and product numbers. The student then enlists the use of the LLM to dervie causal questions that can be evaluated based on this dataset. The LLM posits the following question:

**"Does offering a discount (i.e., reducing the UnitPrice) lead to an increase in the Quantity of products sold for a particular product category?"**

The LLM correctly generated a causal question as it seeks to determine if A creates some change in B such that:
- A: The presence of a known discount (genereated by decreasing the unit price of the items.
- B: The quantitiy of products sold.

The LLM suggested that this question should be analyzed in three parts such that:
- Product Category Identification: Since the dataset provides individual product descriptions but not broad categories, we might consider grouping similar products into makeshift categories based on their descriptions. Alternatively, we could choose a specific popular product as a proxy for its category.
- Discount Identification: We need to identify periods when discounts were offered. This could be done by looking at variations in the UnitPrice for the same product or category over time.
- Effect on Quantity: Once we've identified discount periods, we can compare the Quantity sold during discount periods with that of non-discount periods.

In an effort to streamline the process, the LLM suggested that they generate the analysis based on a specific popular product. While this would enable the analysis to provide a very specific and detailed description it inherently changes the nature of the question. With this method the question would instead be describing if a discount for a specific product then increases sales for the specific product. The student correctly identified that this would be changing the very nature of the question and suggested to the LLM that they instead do an analysis of each of the products.

The LLM accepted this statement, and started the analysis for the top ten products in the list. However, this generates the same issue as disscused previously. The causal question should now be restated:

**"Does offering a discount of the top ten most popular products lead to an increase in the Quantity of these products sold?"**

This question is different from what the student is actually asking, and therefore the resulting analysis will not be complete for any given product, only the top ten products.

The LLM used price fluctuations in each of the products to determine the nature of a "discount". This is a fair assesment if we assume that the price fluctuations are only dependent on the presence of any discount parameter. It does not take into account that the price fluctuations could be based on other confounding variables such as supply chain issues or inflation. It also makes the assumption that the quantity sold is only dependent on price which is not neccessarily the case. Demand is not inherently connected to price and could itself be impacted by confounding variables such as the time of year (Halloween decorations will be bought in massivley different quantities in October than in any other month) or popular trends that influence the psychological perception of demand. The student neglected to consider these possibilites and control for confounders and instead rushed the analysis through a simple model that likely does not very accurretly measures the real world. 

The student then asked the LLM to determine how much more product will be sold for a 10% discount. The LLM created a very simple model that determines how much the quantity sold changes based on the percent discount. Again, the problem plauging this entire analysis is dervied from the fact that the model is not acknolwedging the price and quantity changes based on the entire data set, but rather only the most popular ten products. The LLM identified that some of the popular products will actually see a price decrease given the discount. This makes sense as it failed to acknoledge the counfounders stated above. However, the LLM does posit the following reasons for this interesting and likely inaccurate analysis:

- Price Elasticity: Not all products respond positively to discounts. Some products might have inelastic demand, meaning the quantity sold doesn't increase significantly with a price decrease.
- Perceived Value: Sometimes, lowering the price can affect the perceived value of a product. Customers might associate a higher price with better quality.
- Data Limitations: Our analysis is based on the assumption that changes in price are the only factor affecting the quantity sold. In reality, other factors like promotions, stock availability, seasonality, or external events could impact sales.
- Model Limitations: A linear regression might oversimplify the relationship between price and quantity. More complex models or techniques might provide different insights.

The LLM correctly describes some of the possible reasons for why the model may be innaccurate. It fails to recognize that the question asked by the student is relevant to any given product in the set not just the top ten most popular. The student then takes the answer and ends the analysis without any further inspection of the confounding variables leading to a highly simplifed and likely inaccurate model that answers a different causal question than what is asked.

## Analysis of Data in Order to Create a Funding Pitch
It appears that the student wished to use a LLM to interpertate a data set with a number of key parameters on VC health. The dataset in question revolved around venture capital investments, aiming to offer insights into funding patterns, company profiles, and financial trajectories.

### Loading in The Supplied Data Set
As a part of the data interpretation process, the LLM attempted to load in the supplied CSV file. It threw an error in which it was unable to read the supplied data due to an encoding error. As an attempt to correct the issue, the LLM switched encoding languages and was able to properly load in the data. While this did not create any further challenges in this specific analysis, one could see how had the LLM not known that the encoding format was different it could potentially misinterpret the results failing the analysis from the very beginning.

The LLM then positied various approaches to analyse the dataset:
- Funding by Market: Which markets (industries) receive the most funding?
- Funding Rounds: What are the common funding rounds, and how much funding is typically raised in each round?
- Status of Companies: What is the distribution of company statuses (e.g., operating, acquired) and how does it relate to funding?
- Geographical Analysis: Are there particular regions or countries that attract more venture capital?
- Investment Types: Which types of investment (e.g., seed, venture, equity crowdfunding) are most common?

The student then proceed to prompt the LLM to analyse all of these factors to "get the company funded". While this data can be used to inform a pitch, the operational definition for "get the company funded" needed to be specific based on what possible investors might be looking for in a new company. Without, these defnitions, the LLM will attempt to process the data in a way that is relevant but likely not specific or helpful for an actual pitch.

### Data Cleaning
In an attempt to speed computation, the LLM used a simplified approach to cleaning the data set.  The system replaced any '-' in the 'funding_total_usd' column with '0', a decision that might oversimplify or misrepresent the data. The LLM assumes that '-' signifes zero. But in reality, having missing or unobtainable data is very different from having a value of 0. If the data was infact missing, then the entire relevant row should have been scrubbed. From this mistake in cleaning, the LLM introduced error and artifically changed the nautre of the dataset.

### Analysis
The LLM leveraged the use of visual graphic depictions to highlight trends that might be relevant for a VC pitch. While graphics are useful as a part of the presentaion, they can misrpresent the data to a vast degree depending on how the figure is displayed. For instance if the company had a growth of 10 dollars throughout the last fiscal year, any human would understand that 10 dollars is not that much and does not represent any real growth. However, if one generated a figure in which the y axis was 0.001 dollars, then the growth would appear astronomical and be highly misleading. Given the student did not describe any parameters relevant to how the figures should be displayed or captioned, the pure use of these visuals is not informative. 

The descriptive analyssis approach to creating a pitch is not very complex and does not take into account many of the intracacies of a company that are important to understand when seeking investment. There should be more weight given to inferential statstics, which would attempt to predict where the company is going. As a VC, my pitch would displayed in a way such that I can show how the investors current captial investment will grow over time. Providing data on how the company has grown in the past is innherently inaccurate and unhelpful given that the past did not have the addition of the captial investment inherently changing the parameters of the analysis. Providing a probabilitic model of the future with the proposed investment would be a much more convincing strategy.

Another limitation to this analysis was the fact that the LLM and the student failed to determine if the data uploaded was sufficent enough to even run statistical tests. Ensuring data quality is paramount. It involves verifying that the data is accurate, complete, reliable, relevant, and timely. Without this assessment, any insights derived run the risk of being skewed or misleading. There should have been commentary included on how the data might be limited. If this assumption was made then a ptich could be succesfful but the fact that it was not acknolwedged is very misleading and is bad buisness practice. There was also a lack of identification of any colliders as it can be assumed that any metric of company health will be interconnected. This again results in even a larger skew of the data analysis resulting in a pitch that is not at all relevant to the actual company performance or the risk assesment of the possible investors

##


