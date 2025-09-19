## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1:Create a template with at least two input variables

#### STEP 2:Choose a language model (like GPT-4) to process the prompt.

#### STEP 3:Set up a parser to extract structured data.

### PROGRAM:
```
NAME:V.KASIVISHVANATH
REG NO: 212222040073
```
```
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import ResponseSchema, StructuredOutputParser


# Define the PromptTemplate
prompt = PromptTemplate(
    template="""- Preferred activity: {activity}
- Budget (in USD): {budget}

Make sure the suggested destination is **Switzerland** if possible.  

Provide a response strictly in JSON format.

{format_instructions}
""",
    input_variables=["activity", "budget"],
    partial_variables={"format_instructions": format_instructions},
)

# Define response schema
response_schemas = [
    ResponseSchema(name="destination", description="Recommended travel destination"),
    ResponseSchema(name="activity", description="Suggested activity at the destination"),
    ResponseSchema(name="cost", description="Estimated cost in USD for the trip"),
]

# Create the structured output parser
output_parser = StructuredOutputParser.from_response_schemas(response_schemas)

# Format instructions tell the LLM the exact JSON structure required
format_instructions = output_parser.get_format_instructions()



# Initialize the LLM
llm = ChatOpenAI(model="gpt-4-0613", temperature=0.7)

# Create the chain
chain = LLMChain(llm=llm, prompt=prompt)

# Test the chain with an example
input_data = {"activity": "hiking", "budget": 900}
result = chain.run(input_data)

# Parse JSON into Python dict
parsed_result = output_parser.parse(result)

print("Recommendation:", parsed_result)

```

### OUTPUT:
<img width="1920" height="964" alt="Screenshot 2025-09-19 145717" src="https://github.com/user-attachments/assets/ed741db2-90d5-453f-9d14-9e32c6ee870a" />
<img width="1919" height="965" alt="Screenshot 2025-09-19 145728" src="https://github.com/user-attachments/assets/d3b1639c-3292-4dc3-a2dc-d68f78d990f1" />




### RESULT:Thus, the program is developed and executed successfully to implement a LangChain Expression Language (LCEL) expression that incorporates at least two input parameters and the three essential components—prompt, model, and output parser—while also demonstrating its functionality through analysis of practical real-world examples.
