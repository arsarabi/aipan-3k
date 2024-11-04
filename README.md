# AI-driven Privacy Policy Annotations of Russell 3000 (AIPAN-3k)

This dataset contains AI-generated annotations of privacy policies for companies
in the Russell 3000 index, as described in the paper [Analyzing Corporate
Privacy Policies using AI Chatbots](https://doi.org/10.1145/3646547.3689015).

The dataset consists of 2545 gzipped JSON files, each containing text data and
annotations for a single company in the Russell 3000 index. Files are named
according to the company's Internet domain (e.g., `www.abc.xyz.json.gz`). For
each company, we crawl the associated website to navigate to and scrape privacy
policy pages, and generate structured annotations using OpenAI’s
`gpt-4-turbo-2024-04-09` model.

## Data Structure

Each JSON file contains:
- Text extracted from privacy policy pages.
- Labeled text segments corresponding to different privacy policy aspects.
- AI-generated annotations for four different aspects.

The identified privacy policy aspects are as follows:
- `types`: What types or categories of data are collected.
- `methods`: How data may be collected, including methods, sources, or tools
  used for data collection.
- `purposes`: What are the purposes of data collection, including why data is
  collected and how it is used.
- `handling`: How the collected data is handled, stored, or protected, including
  data processing, retention, and security mechanisms.
- `sharing`: Whether and how data is shared with or disclosed to third parties.
- `rights`: User rights, choices, and controls, including access, edit,
  deletion, and opt-out options.
- `audiences`: Information related to specific audiences, such as children or
  users from specific jurisdictions (California, Europe, etc.).
- `changes`: If and how users will be informed of changes to the privacy policy.
- `other`: Information not covered in the above categories, including
  introductory or generic sections, contact information, and other information
  not directly related to data privacy.
- `all`: Aggregates all of the above aspects excluding `audiences`, `changes`,
  and `other`.

### Text Data Fields

The following fields contain text data and labeled text segments extracted from
privacy policy pages:
- `pages`: A list containing data scraped from privacy policy pages. Each entry
  contains the following fields:
  - `url`: The URL of the page.
  - `text`: The page content in plain text, with some markdown formatting for
    headings.
  - `sections`: A dictionary mapping each privacy aspect to a list of related
    text segments (if any), represented as a list of spans (start and end
    positions) within the `text` field.
- `sections`: A dictionary mapping each privacy aspect to all related text 
  segments across all pages within the `pages` field. Each entry contains the
  following fields:
  - `url`: The URL of the page from which the text segment was extracted.
  - `text`: The specific text segment.
  - `span`: The start and end positions of the text segment within the page.

### Annotation Fields

The following fields contain AI-generated annotations for four of the aspects
described above:
- `types`: Annotations of collected data types, each including a normalized
  descriptor and a category for the data type.
- `purposes`: Annotations of data collection purposes, each including a
  normalized descriptor and a category.
- `handling`: Annotations of data handling practices, including data retention
  periods and specific data protection measures.
- `rights`: Annotations of user rights, including opt-in/opt-out choices and
  privacy settings, and users’ access to view, edit or delete their data.

Each annotation contains the following fields common to all four aspects.
- `url`: The URL of the page from which the annotation was extracted.
- `text`: The annotated text as it appears on the page.
- `category`: The associated category of the annotation.
- `context`: The entire line from which the annotation was extracted.
- `spans`: The list of spans (start and end positions) for the annotation within
  the page text.

In addition to the above, annotations contain the following aspect-specific
fields:
- `types` and `purposes`:
  - `descriptor`: An AI-generated normalized descriptor for the annotation.
- `handling` and `rights`:
  - `type`: Specifies the annotation type, which can be `retention` or
    `protection` for `handling`, and `choice` or `access` for `rights`.
- `handling`:
  - `duration`: For retention periods with a category of `stated`, this field
    indicates the stated retention period.

## Reference

- Ziyuan Huang, Jiaming Tang, Manish Karir, Mingyan Liu, and Armin Sarabi.
  [Analyzing Corporate Privacy Policies using AI Chatbots](https://doi.org/10.1145/3646547.3689015).
  In Internet Measurement Conference (IMC), 2024.
