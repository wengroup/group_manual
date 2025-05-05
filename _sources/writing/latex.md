(label:latex)=

# Using LaTeX

For technical writing, we recommend [LaTeX](https://en.wikipedia.org/wiki/LaTeX), a document typesetting system.

## Getting started

The easiest way to get started is to use [Overleaf](https://www.overleaf.com/), an online LaTeX editor. It is free to use and has a rich set of features.
If you haven't used Overleaf before, you can start with the [Learn LaTeX in 30 minutes tutorial](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes).

Alternatively, you can install a LaTeX distribution on your computer. See [MacTeX](https://www.tug.org/mactex/) for macOS.

## Syntax

Some syntax rules (that are different from other word processors like Microsoft Word) to keep in mind when writing LaTeX documents.

1. Quotes

   The opening and closing quotes are different in LaTeX.
   You should use backticks `` ` `` for opening single quotes, and straight quotes `'` for closing single quotes. Use two backticks ` `` ` for opening double quotes, and two straight quotes `''` for closing double quotes.
   For example, you should write: `` `single quotes'``, which will be typeset as `'single quotes'` , and ` ``double quotes'' `, which will be typeset as `"double quotes"`.

2. Dashes \& Hyphens

   - Hyphen (`-`): Used for compound words, e.g., `state-of-the-art`, `pre-industrial`.
   - En-dash (`--`): Used for ranges, e.g., `1990--2023`, `pp. 45--52`, and to connect related terms, e.g., `New York--London flight`.
   - Em-dash (`---`): Used to indicate interruptions within sentences or to replace parentheses for emphasis. For example, `Indicates interruptions---like this---within sentences` or `Replaces parentheses---though less formally---for emphasis`.

3. Space

   Add a slash `\ ` after a period to indicate that it is not the end of a sentence. For example, you should write `The U.S.\ is a country.`, instead of `The U.S. is a country.`. The period after `U.S.` is not the end of the sentence, so we add a slash `\ ` after it. This will make the spacing between `U.S.` and `is` correct. Similarly, you should use `e.g.\ ` instead of `e.g. ` in the middle of a sentence.

## Tips

LaTex is a powerful typesetting system, and there are a lot of customizations you can make. Here are some tips that we find useful.

1. Write each sentence in a separate line. This makes it easier to navigate long paragraphs using text editors like `vim`, also makes it easier to track changes in `git`.

2. Label your figures, equations, tables, sections, etc. consistently. For example,

   ```latex
   \begin{figure}
       \centering
       \includegraphics{figures/diamond_crystals.pdf}
       \caption{Crystal structure of cubic diamond.}
       \label{fig:diamond}
    \end{figure}
   ```

   It is a good practice to use the prefix `fig:` for figures, `tab:` for tables, `eq:` for equations, `sec:` for sections, etc. This makes it easier to refer to them later in the text.

3. Instead of using `\ref` to refer to figures, equations, tables, sections etc., define your onw macros to customize the reference. Put the below in the preamble of your document.

   ```latex
   \newcommand*{\fref}[1]{Fig.~\ref{#1}}
   \newcommand*{\tref}[1]{Table~\ref{#1}}
   \newcommand*{\eref}[1]{Eq.~\eqref{#1}}
   \newcommand*{\sref}[1]{Section~\ref{#1}}
   \newcommand*{\aref}[1]{Appendix~\ref{#1}}
   ```

   This does nothing but add a prefix to the reference. For example, `\ref{fig:diamond}` will only give `1`. With the above macros, you can use `\fref{fig:diamond}` to get `Fig. 1`.

4. Use `\text{}` for text in math mode. For example, the Boltzmann constant should be written as `$k_\text{B}$`, which gives $k_\text{B}$, instead of `$k_B$`, which gives $k_B$. By default, all text in math mode is italicized. Here `B` stands for the text Boltzmann, and we use `\text{}` to make it upright.

## Useful packages

1. `siunitx` for SI units. For example, the speed of light should be written as `\SI{3e8}{\meter\per\second}`.

2. `mhchem` for chemical formulas. For example, water should be written as `\ce{H2O}`.
