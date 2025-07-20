## `Listening Machine`
An extremely lightweight web-based application designed for provoking reflective cycles in art, culture, and society. Listening machine observes ambient conversation, transcribes it in real-time, and uses an LLM to generate provoking "thoughts" based on what it hears. These insights are then cycled through during the ongoing conversation, adding a layer of interactive contemplation to the environment, a dialogue. 

### Features

-   **Real-time Speech Transcription**: Uses the browser's built-in Web Speech API to capture and transcribe speech.
-   **AI-Powered Reflection**: Periodically sends the transcript to an AI to generate related questions, statements, and connections.
-   **Dynamic Thought Display**: Animates and cycles through the latest set of AI-generated thoughts.
-   **Context-Awareness**: Can be primed with a `context.txt` file to provide background information (e.g., about an exhibition theme or specific artworks) to the AI.
-   **Manual Input**: Includes a text area to simulate speech, allowing for use without a microphone.
-   **Transcript Download**: Allows the user to download a full log of the transcribed conversation and the AI's thoughts.
-   **Secure Configuration**: Keeps your API key out of the main code and version control.

### Getting Started

#### Prerequisites

1.  A modern web browser with support for the Web Speech API (Google Chrome is recommended).
2.  An API key from [Anthropic](https://www.anthropic.com/claude).

#### ⚙️ Configuration

To run the application, you need to provide your Anthropic API key. This can be obtained from the [Anthropic website](https://console.anthropic.com/login?returnTo=%2F%3F), or via a colleague 

1.  **Add Your API Key**: Open the `config.js` file and replace the placeholder text with your actual Anthropic API key.

    ```javascript
    // config.js
    const ANTHROPIC_API_KEY = "sk-ant-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"; // <-- PASTE YOUR KEY HERE
    ```

2.  **Security Note**: The `config.js` file contains your secret API key. **Do not** commit this file to public or private Git repositories. If you are using Git, add `config.js` to your `.gitignore` file.

#### (Optional) Providing Context

You can give the Listening Machine background information to make its thoughts more relevant to a specific topic or environment.

-   Create a file named `context.txt` in the same directory.
-   Add any relevant text to this file—an artist's statement, an exhibition summary, philosophical concepts, etc.
-   The application will automatically fetch this context and include it in its requests to the AI. If the file is not found, it will proceed without it.

#### ▶️ Running the Application

No web server is required. Simply **open the `index.html` file** in your web browser.

1.  **Grant Microphone Access**: The browser will ask for permission to use your microphone. You must allow this for speech transcription to work.
2.  **Start Listening**: Click the "Start Listening" button to begin.
3.  **Interact**: Speak naturally. Your words will appear in the "Transcript" box. After a minute of speech, the "Thoughts" section will update with the AI's reflections.

### 🛠️ How It Works

-   **Frontend**: The entire application runs in the browser using HTML, CSS (Tailwind), and vanilla JavaScript.
-   **Speech-to-Text**: The [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API) listens to the microphone and converts speech into text.
-   **Thought Generation**: At a set interval, the accumulated transcript (and the content of `context.txt`, if present) is sent to the Anthropic API. A carefully crafted prompt instructs the model to return a JSON array of 2-4 short, reflective "thoughts".
-   **API Key**: The API key is loaded from the local `config.js` file and included in the `fetch` request header. This is done directly from the browser, which Anthropic allows for development purposes but is not recommended for production applications where a backend proxy would be more secure.
