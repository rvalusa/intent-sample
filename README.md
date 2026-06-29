# IntentHub Java

IntentHub Java is a complete Android chat application written in Java. It loads a local `.litertlm` model with LiteRT-LM, keeps model selection across launches, and streams assistant responses into a ChatGPT-style Material 3 interface.

## Requirements

- Android Studio latest stable
- JDK bundled with Android Studio
- Android SDK 36 or newer installed
- A LiteRT-LM `.litertlm` model file available on the device

## Build

1. Open this folder in Android Studio.
2. Let Gradle sync and download dependencies.
3. Connect an Android device or emulator running Android 8.0/API 26 or newer.
4. Run the `app` configuration.

## Modules

- `app`: Android application, Material UI, chat RecyclerView, image picker, model file picker, and persisted `.litertlm` model path handling.
- `gemma-ai`: Gemma/LiteRT-LM inference library, model loading from a path supplied by `app`, streaming generation, cancellation, and image decoding for image+prompt inference.

## Usage

1. Tap the folder icon and select a `.litertlm` model.
2. Wait for the model status to show that it is loaded.
3. Type a message and tap send, or attach an image and type a prompt before sending.
4. Prompt-only chats continue to work without selecting an image.
5. Tap stop to cancel an active generation.

## Image Prompts

The chat composer includes an image picker. Selected images appear as a preview before sending and as part of the user message bubble after sending.

Image+prompt inference requires a multimodal LiteRT-LM model and a Java-visible LiteRT-LM generation overload that accepts a `Bitmap` with the prompt. If the loaded model or LiteRT-LM runtime is text-only, prompt-only chat still works and image+prompt requests will show a runtime error.

## LiteRT-LM Notes

LiteRT-LM 0.11.0 is Kotlin-first, and some documentation uses Kotlin-only examples such as `Backend.CPU`. This Java app does not force CPU selection. It lets LiteRT-LM choose the default backend, which avoids the Java visibility issue and keeps backend selection compatible with the published Java bytecode.

The LiteRT integration is isolated in `gemma-ai/src/main/java/com/example/gemmaai/LiteRtManager.java`. If Google changes the Java-facing class names or builder names in a future LiteRT-LM release, update only that module.
