import openai
import os
from dotenv import load_dotenv

# Load the API key from the .env file
load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")

def chat_with_gpt():
    print("Welcome to ChatGPT! Type 'exit' to end the chat.\n")

    conversation = []

    while True:
        user_input = input("You: ")

        if user_input.lower() == "exit":
            print("Goodbye!")
            break

        conversation.append({"role": "user", "content": user_input})

        try:
            response = openai.ChatCompletion.create(
                model="gpt-4",  # Or use "gpt-3.5-turbo"
                messages=conversation
            )

            reply = response["choices"][0]["message"]["content"]
            conversation.append({"role": "assistant", "content": reply})
            print("ChatGPT:", reply)

        except Exception as e:
            print("Error:", e)

if __name__ == "__main__":
    chat_with_gpt()
