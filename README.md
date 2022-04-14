# AMI Data Cleaning Project

## Abstract

This repository contains all the workbooks and datasets related to the AMI data cleaning project undertaken during the R42 data science fellowship. In developed countries, a transition in metering infrastructure is occurring across the utilties sector. Currently, the utilities sector is dominated by [automatic meter reading](https://en.wikipedia.org/wiki/Automatic_meter_reading) technology, in which information regarding consumption levels of a resource is sent to the consumer. [Advanced metering infrastructure](https://en.wikipedia.org/wiki/Smart_meter#Advanced_Metering_Infrastructure) offers several advantages over the current technology, with the main advantages including two-way communication between the supplier and consumer, as well as more granular data, enabling utilities to track usages on a finer basis (hourly reads versus daily reads). 

AMI has a lot of potential, but it also brings with it a number of challenges, with the main one being that the granular data can be messy. By messy, we mean that there are missing/NaN values where there should be actual data. This is an issue because before any predictive models can be built using machine learning, the data has to reflect consumer behaviour. Thus, this project seeks to address how this data can be cleaned to enable further analysis. This repository contains an example AMI dataset reflecting water consumption of over 600 resident over 365 days. It was found that simple interpolation did not clean the dataset sufficiently; during interpolation, the underlying behaviour patterns are being assumed depending on the method of interpolation (linear, quadratic, cubic, etc.). However, none of these methods would reflect the periodicity of the data accurately. By periodicity, we mean cyclical behaviour that repeats with time. 

## Table of Contents

- [Technologies and Libraries](#technologies-and-libraries)
- [Data](#data)
- [Workbooks](#workbooks)
- [Setup](#setup)
- [Introduction](#introduction)
  - [Background](#background)
  - [Opportunity for Data Science](#opportunity-for-data-science)
- [Data Exploration and Visualisation](#data-exploration-and-visualisation)
  - [Hours in a day](#hours-in-a-day)
  - [Months in a year](#months-in-a-day)
  - [Days in a year](#days-in-a-day)
- [Data Cleaning](#data-cleaning)
  - [Import and Load Data](#import-and-load-data)
  - [Unit Conversion](#unit-conversion)
  - [Negative Values](#negative-values)
  - [Missing Values](#missing-values)
  - [Anomalous Values](#anomalous-values)
  - [Interpolate Data](interpolate-data)
  - [Export Data](#export-data)
- [Next Steps](#next-steps)
  - [Short-term Goals](#short-term-goals)
  - [Long-term Goals](#long-term-goals)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

## Setup

To get started, clone this repository to your local machine. Ensure that you have Python installed on your device. Jupyter notebooks can be acquired as an extension on Visual Studio Code or from the Anaconda package.  Please note that the AMI dataset is fairly large (~20MB) and when cells are ran to process this data, the operations may take some time before an output is returned. 

## Technologies & Libraries 

- Python 3.8 or above
- Jupyter Notebooks
- Python Scientific Packages
  - Pandas
  - Numpy
  - Matplotlib
  - Seaborn
  - Sci-kit Learn

## Data

The data used in this analysis has been added to the repository. Please note that it is a large file (>20MB) and contains over 200,000 rows of data relating to hourly consumption of water for a large number of consumers in the Californian state. The data is anonymised, implying that there is no reference to personal information regarding the residents consuming the data. The dataset is made up of a number of columns, with the most pertinent being the columns 2, 3, 4 and 5 which relate to the meter no., datetime stamp, incremental consumption, and cumulative consumption. The meter no. is unique for each resident, and enables us to differentiate between different consumers. The datetime stamp indicates the time and date at which the incremental data was sent. The incremental consumption indicates relatively how much more water the user has consumed since data was lost sent from the meter.  

## Workbooks

A number of workbooks have been added to this repository. 

## Introduction

### Background

Why are we interested in California’s water system in the first place? As we know, water is essential for all consumers. Water is required in our homes as a basic human necessity, for irrigating large agricultural areas of land, for industrial, manufacturing sites and so on. 

If water suppliers and organisations have complete knowledge of incoming water volumes, as well as accurate information on consumer demand, then water suppliers can plan ahead and ensure everyone receives the amount of water they need.  If end-user demand can be accurately predicted, then water districts can procure and deliver a better, more sufficient supply of water to deliver to end-users. This results in:

- Improved water services 
- Lower costs for water districts
- Lower costs for water customers
- Improved water conservation (very important if and when water becomes scarce)

However, California has a complex water system, from widely varying ecosystems for water production to water consumer end-uses.

For clarity, the distinction between water retailers, wholesalers and districts is made:

- Water retailers manage customer-side issues, issues bills, collect payment and water readings and upload these into the water market’s central database. 
- Water wholesalers manage network issues, manage the installation and maintenance of water meters and respond to leakages and meter issues (sending out someone to fix - the issue at the property).
- Water district is given the task of supplying water and sewage needs to a community. 

Therefore, a water district can be described as a retailer and wholesaler combined. The function of the district may vary on a district-by-district basis. End-user (consumer) demand can be a challenge for water districts. This is because:

Water meters are currently installed as part of an AMR (automatic meter reading) infrastructure, which automatically collects consumption on a monthly basis. 
On AMR systems, predictions for consumer demand can only be made on a monthly basis, and the water supplied from these predictions may not satisfy peak flow, as daily usage will fluctuate. 

Further complications to predicting end-user demand include:

- California recently experienced a large drought (2014-2016) and may be entering another. Drought events have had a huge impact on water behavior, breaking many older water models by changing the assumptions behind them. 
- COVID-19 has drastically impacted water behavior, moving much of the water end use to residential locations rather than in businesses, further complicating water district’s models.

### Opportunity for Data Science

Water districts have millions of rows of historical data on production and consumption.

- What can be done with all this historical data?

On the consumption side, years of historical datasets can be cleaned and analysed to produce customer insights. From these insights, the districts can improve understanding of their customer base, which can help districts deliver a stronger supply of water to their customers. For instance, if districts learn how consumers responded to drought or the COVID-19 lockdown restrictions, they can plan better if these situations repeat in the future. 

On the production side, retailers, wholesalers, and other water organizations rely heavily on using weather forecasting with watershed models to predict incoming water volumes.

- Can this process be improved? 
- Can it be integrated with an end use model for an “all-in-one” model?

Furthermore, new infrastructure in the form of Advance Metering is being installed in several districts giving access to very granular water data (up to readings every 15 mins) at the end use. This poses the following question:

- How can AMI data be best used? 

New data analytical techniques can be developed with the more granular data to better predict consumer demand. This will involve leveraging data science applications such as python packages, like pandas and SciPy, or other software packages. Here, there is a potential to learn more about how different customers (residential, commercial, industrial, etc.) consume water on a daily and weekly basis. 

- Can new behavioral models be created?

A particular analytical technique that can be applied is customer segmentation, where water consumers that display similar consumption characteristics will be grouped. This makes it easier for a water district to identify who is using water, how it’s being used and designate consumers to a group, all of which will help to predict demand. 

- Can the data be used to assess leakages? 

On the AMR system most districts are currently using, you can only detect and fix a leak on the network after a long time, like a week or, at worst, a month. This means there’s a potential for a lot of water to be lost, reducing business revenue. However, with newer AMI systems, leaks can be detected much sooner, saving districts revenue and improving water conservation. 

- How can older mechanical water use and water savings models be remade with a more dynamic basis?

Water data science is not as far along as many other industries, and this is in part due to a lack of data centralization, data is hard to get.

- How can we improve this, and bring the data together?

The water industry is ripe with data questions and is a prime opportunity to use what has been learned in other data arenas and apply it to a new set of problems. Furthermore, lessons learnt from the water industry can possibly be applied in other sectors, where perhaps organisations are reluctant to engage in Industry 4.0 (automation of manufacturing using smart tech). 

## Data Exploration/Visualisation

## Data Cleaning

### Linear Interpolation

### Fast Fourier Transform

## Next Steps

### Short-term Goals

### Long-term Goals

## License

The license for this repository can be found [here](#LICENSE.md)

## Acknowledgements 

Thanks to [Russ](https://www.linkedin.com/in/russhp/) for being my mentor on this project and teaching me the fundamentals of programming. 

## Contact

Please reach out to me on [LinkedIn](https://www.linkedin.com/in/fahmidul-haque-b7a96b123/) for any questions regarding this repository. 

