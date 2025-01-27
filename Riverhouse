import openai
import streamlit as st

# Set up the OpenAI API key (this will be pulled from Streamlit Secrets)
openai.api_key = st.secrets["OPENAI_API_KEY"]

# Streamlit app title
st.title("Related Words Generator")

# Get user input
word_input = st.text_input("Enter a word to find related words:")

# Function to fetch related words from OpenAI
def get_related_words(word):
    try:
        # Send a prompt to OpenAI to generate related words
        prompt = f"Provide 5 common or related words to '{word}'."
        response = openai.Completion.create(
            model="text-davinci-003",
            prompt=prompt,
            max_tokens=50,
            temperature=0.7
        )
        
        # Parse the result
        related_words = response.choices[0].text.strip().split(',')
        
        # Clean and return the related words
        return [word.strip() for word in related_words]
    
    except openai.error.OpenAIError as e:
        st.error(f"Error with OpenAI API: {e}")
        return []

# Display related words
if word_input:
    st.subheader(f"Related words for '{word_input}':")
    related_words = get_related_words(word_input)
    if related_words:
        st.write(", ".join(related_words))
    else:
        st.write("No related words found.")
