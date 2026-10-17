# AI Interface

## 1. Function Signature

```typescript
translateText(input: TranslationInput): TranslationResult
```

## 2. Input

```typescript
interface TranslationInput {
  text: string;
  sourceLanguage: string;
  targetLanguage: string;
}
```

## 3. Output

```typescript
interface TranslationResult {
  success: boolean;
  translatedText?: string;
  error?: string;
}
```

## 4. Errors

- `INVALID_INPUT`: Input is empty.
- `UNSUPPORTED_LANGUAGE`: Language is unsupported.
- `MODEL_UNAVAILABLE`: Local translation model is unavailable.
- `TRANSLATION_FAILED`: Translation fails.

## 5. Fallback

- Invalid input: Return `INVALID_INPUT`.
- Unsupported language: Return `UNSUPPORTED_LANGUAGE`.
- Model unavailable: Return `MODEL_UNAVAILABLE`.
- Translation failure: Return `TRANSLATION_FAILED`.
- No Internet: Do not switch to an online service.

No LLM or translation model is called or implemented in this task.
