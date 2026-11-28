# Sweet Crumbs Home Bakery -- AI Order Assistant

## Overview

This notebook builds a conversational AI assistant for **Sweet Crumbs
Home Bakery**. It can answer customer questions about menu prices and
opening hours, collect cake-order details, calculate order totals, and
save confirmed orders to a Google Sheet.

## Features

-   Conversational ordering using a Groq-hosted language model through
    LangChain.
-   Menu price lookup for plum cake, chocolate cake, and cupcakes.
-   Opening-hours lookup for each day of the week.
-   Structured order validation with Pydantic.
-   Saves confirmed orders to a Google Sheet.
-   Maintains conversation history during the notebook session.
-   Supports English or Telugu responses, as requested in the system
    prompt.

## Technologies

-   Python
-   LangChain and `langchain-groq`
-   Groq API (`openai/gpt-oss-20b`)
-   Pydantic
-   Google Colab authentication
-   Google Sheets via `gspread`

## Notebook

Open and run `class4.ipynb` in Google Colab.

## Setup and Execution

1.  Upload `class4.ipynb` to Google Colab.

2.  Install the notebook dependencies:

    ``` python
    !pip install -q langchain langchain-groq gspread
    ```

3.  In Google Colab, add a secret named `GROQ_API_KEY` containing your
    Groq API key. Do not hard-code or publish the key.

4.  Run the cells in order.

5.  Complete Google authentication when prompted and grant access to
    Google Sheets.

6.  The notebook creates a spreadsheet named **Sweet Crumbs Orders** and
    adds the order table headers.

7.  Use the `chat()` function to talk to the assistant and place orders.

## Menu and Business Rules

  Item               Price
  ---------------- -------
  Plum cake           ₹500
  Chocolate cake      ₹650
  Cupcake              ₹80

-   Orders require 24 hours' notice.
-   Eggless versions are available for all cakes.
-   Opening hours are 9 AM--8 PM Monday through Saturday and 10 AM--6 PM
    Sunday.

## Order Data Saved

The Google Sheet stores: `name`, `item`, `qty`, `date`, `eggless`, and
`total`.

## Example

``` python
print(chat("Are you open on Sunday? How much are 2 chocolate cakes?"))
print(chat("I'm Ravi. Please book 2 eggless chocolate cakes for 24 Dec."))
```

## Notes and Limitations

-   The notebook uses Google Colab-specific authentication and secret
    management; it is not configured as a standalone local application.
-   The spreadsheet is created when the setup cell runs. If it already
    exists, open it by name instead of creating another copy.
-   The notebook's menu, prices, and hours are defined in Python
    dictionaries and must be updated there when business details change.
-   Test the order flow with non-production data before using it for
    real customer orders.
-   Never commit API keys, credentials, or private customer information
    to a public repository.

## Project Structure

``` text
project/
├── class4.ipynb
└── README_class4.md
```
