# Build Neural Networks in TypeScript

> A from-scratch walkthrough of a tiny neural network in TypeScript, using XOR to teach forward passes, backpropagation, and the matrix math underneath.

- **Speaker:** Junichi Takahashi, raindrops
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=rX14bHH5wI0) (AI Engineer channel; ~14m, released 2026-06-22)
- **Program:** Online Track 2026

## Summary

Junichi Takahashi, a software engineer in Tokyo, builds a working neural network in TypeScript with no ML libraries, aimed at engineers who use AI daily and want to see how learning actually happens inside a model. His running example is XOR, the classic case that looks trivial and yet cannot be separated by a single straight line, which makes it a compact argument for why networks need multiple layers.

Takahashi contrasts two implementations. The hardcoded version is a two-line TypeScript function that returns whether two booleans differ. The learned version never states the rule at all. It multiplies inputs by weights, adds biases, and passes the result through a sigmoid activation, and the correct behavior emerges from adjusting those weights against data. He walks a concrete forward pass: an input produces a pre-activation value of 0.6, sigmoid squashes it to roughly 0.65, and that becomes the layer output. The code centers on a small Tensor class that handles the matrix work.

The middle of the talk is a plain-language tour of backpropagation. With an output of 0.65 against a target of 1.0, Takahashi computes squared error, explains why the conventional one-half factor exists (it cancels when you differentiate), and derives the output gradient as y minus t. He then chains that gradient backward: through the sigmoid using its derivative y times (1 minus y), then to the weights via the transposed input, to the previous layer via the transposed weights, and to the bias directly. Updates subtract the learning-rate-scaled gradient because the gradient points toward higher error. He flags the standard failure modes: a learning rate too large is unstable, too small is slow.

Takahashi then shows training converge. Early outputs hover near 0.4 or 0.5, essentially guessing. After repeated updates the network lands around 0.01 for the false cases and 0.98 for the true ones, so it has learned XOR from data rather than from a rule. A single layer cannot get there, he notes, because it can only draw a linear boundary. The first layer transforms the input into a new feature space and the second layer separates it.

The last third fills in the math prerequisites at the same deliberate pace: deriving the derivative of x squared from first principles by shrinking h toward zero, then each Tensor operation in turn. Element-wise add, subtract, and multiply, matrix multiplication as rows-times-columns with a worked 2x2 example, transpose (used heavily in backprop), and scaling (used to apply the learning rate). He closes on why sigmoid uses Euler's number: the natural exponential keeps the derivative clean, which keeps the training loop code simple. The full source, plus CNN and RNN examples, is in a GitHub repository he shows at the end.

The talk makes no claims about production practice. It is a teaching session, and its quiet premise is that the language barrier between web engineers and ML fundamentals is smaller than it looks: a few hundred lines of TypeScript cover the whole loop.

## Notable moments

- [0:02:05](https://www.youtube.com/watch?v=rX14bHH5wI0&t=125s) The forward pass by hand: weights, bias, and sigmoid turning 0.6 into 0.65.
- [0:05:05](https://www.youtube.com/watch?v=rX14bHH5wI0&t=305s) Backpropagation as the chain rule applied to a chain of functions, mapped to the code's backward method.
- [0:07:06](https://www.youtube.com/watch?v=rX14bHH5wI0&t=426s) Why one layer cannot solve XOR and stacking layers fixes it.
- [0:13:13](https://www.youtube.com/watch?v=rX14bHH5wI0&t=793s) Training results near 0.01 and 0.98, plus the GitHub repo with CNN and RNN examples.

## Connections

No company profile or paper note in this repo covers ML-fundamentals education or the speaker's company; the closest thematic neighbor in the video set is Roberto Stagi's talk on TypeScript as the language of the AI application layer, filed alongside this one in talks/videos/.
