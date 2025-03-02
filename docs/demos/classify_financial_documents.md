---
layout: demopagenew
title: Classify Financial Documents - Finance NLP Demos & Notebooks
seotitle: 'Finance NLP: Classify Financial Documents - John Snow Labs'
subtitle: Run 300+ live demos and notebooks
full_width: true
permalink: /classify_financial_documents
key: demo
nav_key: demo
article_header:
  type: demo
license: false
mode: immersivebg
show_edit_on_github: false
show_date: false
data:
  sections:  
    - secheader: yes
      secheader:
        - subtitle: Classify Financial Documents - Live Demos & Notebooks
          activemenu: classify_financial_documents
      source: yes
      source: 
        - title: ESG News Classification  
          id: esg_news_classification       
          image: 
              src: /assets/images/ESG_News_Classification.svg
          excerpt: This demo showcases ESG news classification, with 3-classes and 27-classes ESG models.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/FINCLF_ESG/
          - text: Colab
            type: blue_btn
            url: 
        - title: Financial News Classification 
          id: financial_news_classification        
          image: 
              src: /assets/images/Financial_News_Classification_new.svg
          excerpt: This model classifies financial news using multilabel categories.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/CLASSIFICATION_MULTILABEL/
          - text: Colab
            type: blue_btn
            url:         
        - title: Identify topics about banking
          id: classify_banking_related_texts   
          image: 
              src: /assets/images/Classify_Banking-related_texts.svg
          excerpt: This demo shows how to classify banking-related texts into 77 categories.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/public/CLASSIFICATION_BANKING/
          - text: Colab
            type: blue_btn
            url: https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/streamlit_notebooks/BertForSequenceClassification.ipynb
        - title: Classify Customer Support tickets (banking)  
          id: classification_bank_complaint_texts      
          image: 
              src: /assets/images/Classification_of_Bank_Complaint_Text.svg
          excerpt: This model classifies the topic/class of a complaint about a bank-related product.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/COMPLAINT_CLASSIFICATION/
          - text: Colab
            type: blue_btn
            url: https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/streamlit_notebooks/BertForSequenceClassification.ipynb
        - title: Forward Looking Statements Classification 
          id: forward_looking_statements_classification       
          image: 
              src: /assets/images/Forward_Looking_Statements_Classification.svg
          excerpt: This demo shows how you can detect Forward Looking Statements in Financial Texts, as 10K filings or annual reports.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/FINCLF_FLS/
          - text: Colab
            type: blue_btn
            url:  
        - title: Analyze sentiment in financial news
          id: analyze_sentiment_financial_news 
          image: 
              src: /assets/images/Analyze_sentiment_in_financial_news.svg
          excerpt: This demo shows how sentiment can be identified (neutral, positive or negative) in financial news.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/public/SENTIMENT_EN_FINANCE/
          - text: Colab
            type: blue_btn
            url: https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/streamlit_notebooks/SENTIMENT_EN_FINANCE.ipynb
        - title: Receipt Binary Classification
          id: receipt_binary_classification 
          image: 
              src: /assets/images/Receipt_Binary_Classification.svg
          excerpt: This demo shows how to use ViT, a Visual Transformer, to identify receipts vs no receipts in an image corpus.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/RECEIPT_BINARY_CLASSIFICATION/
          - text: Colab
            type: blue_btn
            url: https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/streamlit_notebooks/finance/RECEIPT_BINARY_CLASSIFICATION.ipynb
        - title: Classify Earning Calls, Broker Reports and 10K
          id: classify_earning_calls_broker_reports_10k 
          image: 
              src: /assets/images/Classify_Earning_Calls_Broker_Reports_and_10K.svg
          excerpt: This is a Text Classification model, which can help you identify if a model is an Earning Call, a Broker Report, a 10K filing or something else.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/FINCLF_EARNING_BROKER_10K/
          - text: Colab
            type: blue_btn
            url: 
        - title: Classify Different SEC Filings
          id: classify_different_sec_filings 
          image: 
              src: /assets/images/Classify_Different_SEC_Filings.svg
          excerpt: This demo showcases how to use pretrained Finance NLP models to classify SEC filings (10-K, 10-Q, 8-K, 3, 4 and S-8) documents.
          actions:
          - text: Live Demo
            type: normal
            url: https://demo.johnsnowlabs.com/finance/FINCLF_SEC_FILINGS/
          - text: Colab
            type: blue_btn
            url: 
---