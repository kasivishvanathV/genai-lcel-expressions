## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
Design and integrate a Python function that calculates the volume of a cylinder, and enable the function to be called through a chat completion system, simulating an LLM interface.
## DESIGN STEPS:  
1. **STEP 1:** Create a prompt template with placeholders for at least two parameters.  
2. **STEP 2:** Use LangChain's language model to process the prompt and generate a response.  
3. **STEP 3:** Implement an output parser to extract structured results from the model's response.


### PROGRAM:
Name:Kasivishvanath V
Reg No:212222040073
```
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import ResponseSchema
from langchain.schema.output_parser import StrOutputParser

# Define the PromptTemplate
prompt = PromptTemplate(
    template="""
You are a travel assistant. Based on the following inputs, recommend a destination:
- Preferred activity: {activity}
- Budget (in USD): {budget}

Provide a response strictly in JSON format:
{{
    "destination": "<destination>",
    "activity": "<activity>",
    "cost": "<cost>"
}}
""",
    input_variables=["activity", "budget"],
)

# Define the Output Parser
response_schemas = [
    ResponseSchema(name="destination", description="Recommended travel destination"),
    ResponseSchema(name="activity", description="Suggested activity at the destination"),
    ResponseSchema(name="cost", description="Estimated cost in USD for the trip"),
]
output_parser = StrOutputParser()

# Initialize the LLM
llm = ChatOpenAI(model="gpt-4-0613", temperature=0)

# Create the LangChain Expression (LLM Chain)
chain = LLMChain(llm=llm, prompt=prompt, output_parser=output_parser)

# Test the chain with an example
input_data = {"activity": "hiking", "budget": 1000}
result = chain.run(input_data)

# Parse the structured output
parsed_result = output_parser.parse(result)

# Display the result
print("Recommendation:", parsed_result)
`````
### OUTPUT:
![Screenshot (196)](https://github.com/user-attachments/assets/96a1febe-d68c-4e18-bcf9-3e7c2721ac1b)


### RESULT:
Hence,the program to design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios is written and successfully executed.
