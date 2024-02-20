<br/>
<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="image/abacus_logo_dark.png">
  <source media="(prefers-color-scheme: light)" srcset="image/abacus_logo.png">
  <img src="image/abacus_logo.png" width=800>
</picture>
</p>
<p align="center"><img src="image/smaug_dragon.png" width=500 /></p>

----

Smaug arrives!

We recently released [Smaug-72B-v0.1](https://huggingface.co/abacusai/Smaug-72B-v0.1) which has taken first place on the Open LLM Leaderboard by HuggingFace. It is the first open-source model to surpass an average score of 80%, and it is nearly 2% better than the next-best open-source model. We also released [Smaug-34B-v0.1](https://huggingface.co/abacusai/Smaug-34B-v0.1), the best 34B model at the time of its release. 

We created both models using a new fine-tuning technique, DPOP, and new pairwise preference versions of ARC, HellaSwag, and MetaMath. We introduce both the technique and the datasets in our new arXiv paper: xxxxxx.

We give theoretical and empirical evidence for a failure mode in the standard DPO loss: on datasets in which the edit distance between pairs of completions is low (such as in math-based datasets), standard DPO loss can lead to a _reduction_ of the model's likelihood of the preferred examples, as long as the relative probability between the preferred and dispreferred classes increases. Using these insights, we design DPO-Positive (DPOP), a new loss function and training procedure which avoids this failure mode. Surprisingly, we also find that DPOP significantly outperforms DPO across a wide variety of datasets and downstream tasks, including datasets with high edit distances between completions. Using DPOP, we create Smaug-34B-v0.1 and Smaug-72B-v0.1, which achieve state-of-the-art open-source performance.

<p align="center"><img src="image/dpop_overview.png" width=700 /></p>

## Smaug-72B-v0.1

[Smaug-72B-v0.1](https://huggingface.co/abacusai/Smaug-72B-v0.1) is finetuned directly from [moreh/MoMo-72B-lora-1.8.7-DPO](https://huggingface.co/moreh/MoMo-72B-lora-1.8.7-DPO) and is ultimately based on [Qwen-72B](https://huggingface.co/Qwen/Qwen-72B).

### HuggingFace Open LLM Leaderboard Results

| Average | ARC | HellaSwag | MMLU | TruthfulQA | Winogrande | GSM8K |
| --- | --- | --- | --- | --- | --- | --- |
|  80.48  | 76.02 | 89.27  | 77.15 | 76.67 | 85.08 | 78.70 |

#### MT-Bench

We ran MT-Bench with the llama-2 conversation template and the system prompt set to the Qwen system prompt. We got the following
results in single model mode:

| First Turn | Second Turn | Average |
| ---------- | ----------- | ------- |
| 8.18       | 7.34        | 7.76    |

The bottom of the card includes some sample responses from the model. We have selected responses that have high and low scores
from the GPT-4 judge.

### Contamination Results

We generate our contamination numbers using https://github.com/swj0419/detect-pretrain-code-contamination/tree/master, with Llama7B as our reference model.
Smaug-72B has the following results:

| ARC | TruthfulQA | GSM8K |
| --- | --- | --- |
| 0.20| 0.45| 1.00|

By comparison, MoMo-72B-lora-1.8.7-DPO has the following results:

| ARC | TruthfulQA | GSM8K |
| --- | --- | --- |
| 0.20| 0.39| 1.00|

Note that GSM8K often scores very highly on this contamination suite - we verified this by also running Llama-2-70B:

| ARC | TruthfulQA | GSM8K |
| --- | --- | --- |
| 0.22| 0.51| 0.89|


### Sample MT Bench results

#### Example 1
**Question**

Imagine you are writing a blog post comparing two popular smartphone models.
Develop an outline for the blog post, including key points and subheadings to effectively
compare and contrast the features, performance, and user experience of the two models.
Please answer in fewer than 200 words.

**Response**

Outline:

1. Introduction to the two smartphone models being compared (mention brand names and models)
2. Design and Build Quality
   - Comparison of dimensions, weight, materials used, and overall aesthetic appeal
   - Water and dust resistance, if applicable
3. Display and Screen Quality
   - Comparison of screen technology (OLED, IPS LCD, etc.)
   - Display resolution, refresh rate, and brightness levels
4. Performance and Hardware
   - Processor, RAM, and storage configurations
   - Comparison of benchmark scores (e.g., AnTuTu, Geekbench)
5. Camera System and Image Quality
   - Comparison of primary, ultra-wide, telephoto, and macro lenses (if available)
   - Comparison of low-light performance and image processing capabilities
6. Battery Life and Charging
   - Battery capacity and estimated usage time
   - Charging technologies (wired, wireless, fast charging, reverse charging)
7. Software and User Experience
   - Comparison of operating systems (iOS vs. Android) and their features
   - User interface, customization options, and app ecosystem
8. Additional Features and Extras
   - Comparison of biometric authentication (fingerprint, face unlock, etc.)
   - Additional features like NFC, 5G connectivity, and audio quality
9. Pricing and Value for Money
   - Comparison of retail prices and current offers
   - Assessment of overall value considering the features and performance
10. Conclusion and recommendation for potential buyers based on their preferences

#### Example 2
**Question**

In a survey conducted at a local high school, preferences for a new school color were measured: 
58% of students liked the color blue, 45% preferred green, and 22% liked both colors.
If we randomly pick a student from the school, what's the probability that they would like neither blue nor green?

**Answer**

To find the probability that a randomly picked student would like neither blue nor green, we need to find the percentage of students who like only one color or neither color.

From the given information, we know:
- 58% like blue
- 45% prefer green
- 22% like both colors

To find the percentage of students who like only one color, we can subtract the percentage of students who like both colors from the sum of students who like blue and green:
- 58% (blue) + 45% (green) - 22% (both) = 83%

Now, to find the probability of a student liking neither blue nor green, we subtract the percentage of students who like at least one color from 100%:
- 100% - 83% = 17%

So, the probability that a randomly picked student would like neither blue nor green is 17%.

#### Example 3
**Question**

Implement a program to find the common elements in two arrays without using any extra data structures.

**Answer**

Finding common elements in two arrays without using extra data structures can be achieved by using a simple algorithm. Here's a Python implementation of this problem:

```python
def find_common_elements(arr1, arr2):
    common_elements = []
    for num1 in arr1:
        if num1 in arr2 and num1 not in common_elements:
            common_elements.append(num1)
    return common_elements
# Example usage:
array1 = [1, 2, 3, 4, 5]
array2 = [4, 5, 6, 7, 8]
print(find_common_elements(array1, array2))  # Output: [4, 5]
```

This program iterates through the elements of the first array (arr1) and checks if each element is present in the second array (arr2). If it is, and the element hasn't been added to the common_elements list yet, it is appended. The function then returns the list of common elements.
#### Example 4
**Question**

Identify the named entities (people, organizations, locations) mentioned in the given news article.
Please generate a JSON dictionary that lists the named entities in three separate groups based on their entity types.
The key is the type of entity and the value is a list of strings.
Yesterday, Adamson Emerson, the CEO of Faraday, and Dieter Zetsche, the CEO of Daimler AG, announced plans to
build a new Gigafactory in Berlin. The facility will be a joint venture between Faraday and Daimler, producing
electric vehicles and battery packs for both companies, creating thousands of job opportunities in the region.
Emerson and Zetsche stated that the strategic location of Berlin, coupled with its skilled workforce and strong infrastructure,
makes it an ideal choice for expansion. The new Gigafactory aims to meet the growing demand for electric vehicles in Europe
and contribute to a sustainable future. Volkswagen CEO Herbert Diess welcomed the news, saying greater collaboration will,
benefit the auto industry's transition to e-mobility.

**Answer**

```
{
  "people": ["Adamson Emerson", "Dieter Zetsche", "Herbert Diess"],
  "organizations": ["Faraday", "Daimler AG", "Volkswagen"],
  "locations": ["Berlin", "Europe"]
}
```

