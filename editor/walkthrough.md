## Separate packet jitter from a fixed clock offset

Returns [transit range, smoothed jitter, adjacent pairs]. Input rows must be in arrival order and use unwrapped sender timestamps. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `cormorant-demo.blyx`.
2. Type `blyx-cormorant-demo` and select **Cormorant — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
32
2
1
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-cormorant)
