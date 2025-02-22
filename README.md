## Title: Study of the Biggest Leak in 

#### Web site:
The data story is available [here](https://elleuchkh.github.io/)

#### Abstract:

The Panama Papers involved hundred thousands of offshore accounts, millions of documents detailing top secret financial information were leaked in 2015 by an anonymous source. It is estimated that tax havens cost poor countries at least $170 billion in lost tax revenues each year making poorest people lose out and the inequality gap grow. Holding money in an offshore company is generally not illegal but it can be used to launder money, dodge sanctions, avoid taxes. Many people listed in the panama papers claimed being innocent. There is a huge amount of data, our work will be to provide a detailed analysis of the dataset. We will not focus our analysis on individuals but we will instead  be getting a closer view about the involved countries and the distribution of the papers  around the world and trying to find any correlation between the implication of each country in the panama papers with other finacial studies such as Financial secrecy index, Corruption ... and with any other interesting information we could get about those countries. 


#### Researchs questions: 
- What are the top countries that have the most number of relationship with suspicous intermediaries? 
- what is the distribution of officers, entities and intermediaries around the world? It is based in specified countries or it is overspreaded? 
- Can we relate our rankings to other world known indicators? 
- What is the effect of suspecious investments on some countries? (Espcially top Tax havens)
- Does Mossack Fonseca have connections with entities (intermediary companies, clients, beneficiaries and shareholders) based in countries which had a high degree of illicit outflows?
#### Dataset:
- Panama papers

Unfortunately, we don't have access to big part of the data and metadata from the original leaks so we decided to enrich our data with other similar datasets found in ICIJ (The International Consortium of Investigative Journalists):
    - Paradise papers
    - Offshore leaks
    - Bahamas leaks
    
The hybrid dataset is composed of four parts: 

    * Entities: is a company, trust or fund created in a low tax offshore jurisdiction.
    * Officers: a person or a company who plays role in an offshore entity.
    * Intermediairies: the link between someone seeking an offshore and an offshore service provider.
    * Addresses: description of the addresses contained in the dataset.
    * Edges: they connect nodes from the above parts and describe the nature of the relation between them, 
      it's has three important features 'registered address', 'beneficiary of' and 'intermediary of'.
     
#### Internal milestones up until milestone 3:
- Data collection:
    We will add to Panama papers Bahamas Papers, Paradise papers and offshore papers to have more entries.                         Searching for other datasets related to financial statistics and corruption around the world: 
    - CPI: Courrption Perception Index
    - FSI: Financial Secrecy Index
- Cleaning data: 
    - Concatenate entries from Panama papers, Bahamas Papers, Paradise papers and offshore papers and try to have 4 clean datasets related to entities, officers, intermediaires and edges. 
      
    - Add new columns, if needed, to identify the natures of each node {entity, addresse, intermediary, officer}.
    
    - Since our analysis will focus on countries, match node id's to the their country name. 
    
    - Country names needed to be cleaned, some rows contains multiple names of countries. An expansion of rows would be a good idea. 
      
    - Finally, save the cleaned dataframes in a new folder to use them for data wrangling and exploitation.
    
- Data wrangling: 
    To get more familiar with our data, some plots should be used to have an idea about the different aspects of our datasets: 
    - Plot the counts of entities, officers and intermediairies per each country in a stacked format.
    
    - Active intermediaries are also interresting. A plot may help us understand how the network was connected at the last time snapshot.
      
    - The evolution over time of the entities is also important to be visualised. It shows us when does this suspicious 
     activity has grown in time.
     
     - A folluim map with entities, intermediares and officers country counts is shows to highlight the distribution of the network on a world map.

  
- Network Analysis: 
    - first approach: 
    
      - A graph created with the name of the country as the indentifiant of the node.

      - The Degree Centrality algorithm is employed to see the importance of the nodes of the graph which in our case
      are countries.

      - The Page Rank algorith is also used to check the importance of countries based on the incoming link which will 
      help identify the countries with most important numbers of entities, intermediaries and officers.

      - Betweenes centrality algorithm served to detect nodes that serves more as bridges, this algorithm brought to light a new set of countries that does not figures analysis or it improved remarkably theire ranking such as Panama, Jersey. Others countries do not figures in top ten, one example is Russia.

      - To understand and to figure the nature of those relations between countries we use the edge betweenness centrality which basicaly gives us the importance of edges in the graph. The results surprised us since we expected that the most important edges will be between countries that appeared earlier in our analyis but a new set of countries came into the field. Some of those edges are (Switzerland, Mali), (Hong Kong, Namibia). Those edges made us consider that maybe shady business in countries such as Namibia are maybe runned by entities in Hong Kong.
      
    - Second approach:
     
      - To enhance our analyis, we created a new bipartite graph which in one hand contain the node_id and in the other hand the countries names. 
      
      - The main objective of creating such graph is to highlight the importance of connections between countries, to do so we projected our graph into a new weighted graph. If more than one node is connected to two country the new weighted graph will set the weight as the number of those related nodes.
      
    - Third approach:
    
      - At this step we created a graph with node_id, the aim of this approach is to see how a country can be linked to an other country via multiple nodes. 
      
      - First we computed the longest path in our graph.
     
      - Second the path nodes id were mapped to theire corresponding countries and edges to their corresponding types. 
      
      - Finally, we noticed that an entity can be based in different countries, so we used this to create different paths. One path example is: ['British Virgin Islands', 'Singapore', 'Thailand', 'Indonesia']. 

      - The previous analysis proves that a fraction of one country businesses  is managed by an other country. Also, the fact that there is multinational entities and officers that operates in multiple countries make our dataset more interesting and confusing at the same time.
      

- Network visualisation:
    - Our dataset represents connections between countries according to a set of attributes (Entities, officers and intermediairies). One of our goals was to visualize those connections and implement a robust code that will help us switch attributes and visualize as much as possible of specific connections.
    
    - The next challenge was to see how those attributes were connected arround the world. For our analysis and to be able to have a nice visulaisation we decided to consider connections between Switzerland and other countries since Switzerland is one of the countries that have an important number of entities in it's territory.
    For this analysis we used the basemap library which have a nice visualisation features. However, in the notebook you can see how Switzerland entities are connected to world entities.
    
    - The last challenge of our visualization study was to put together all connections between the countries using the  graph generated by the projection of the bipartite graph generated in network analysis. To make our last graph be generic and highly sophisticated and intereactive we requested a API key from graphistry which helped us to much for our visualization analysis.
    

- Correlation to world indicator, Financial Secrecy Index:

    - We wanted to find any correlation between the implication of each country in the panama papers with official indexes published by world wide organizations. 
    
    - We worked with the pearson correlation because we were intereseted in the rank correlation not the values.
    
    - We computed the correlation with the count of the 3 categories of involved countries (entities, officers and intermediaries). Also, we studied the correlation with  the network properties to be more sure.
    
    - We removed Outliers when neccessary.
    
    - All the correlations were between 0.6 and 0.7 which is a satisfying result : That means that the countries having a good ranking regarding Financial Secrecy Index (FSI) attract more offshore entities
  

#### Run the code:

To be able to run the code you need to unzip the compressed files:
- big_data_to_compress.tar.gz
- data_cleaned.tar.gz
- data_follium.tar.gz

#### Resources:
- www.gfintegrity.org illicit financial flows from developing countries.
- https://www.financialsecrecyindex.com/ financial secrecy index.
- https://www.transparency.org/research/cpi/overview corruption perception index.
- https://www.kaggle.com/unsdsn/world-happiness Happiness index.
