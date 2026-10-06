# Learning How AI Agents Work by Building Them

Replication material for the paper *Learning How AI Agents Work by Building Them: A Pre/Post Study of an
Agentic Engineering Lab* by Steffen Herbold, Fabian C. Peña, Lukas Schulte, and Gordon Fraser.

The study measures what students learn about how AI agents are implemented during a three-week lab in which
they build an agentic coding harness. Students completed a paper questionnaire at the start and at the end of
the lab. Each questionnaire has three parts:

- **Part A**: demographics and prior experience (pre-test), and what the student did during the lab
  (post-test).
- **Part B**: self-assessment of the learning objectives and the harness components, with identical wording
  in both waves.
- **Part C**: a 20-item multiple-choice quiz. The quiz exists in two parallel forms, A and B, and the order
  of the forms is counterbalanced: half of the students take Form A in the pre-test and Form B in the
  post-test, the other half the reverse.

## Repository structure

```
tasks/
  main.tex                                      planning document of the lab
survey/
  pre_form_a.tex   pre_form_b.tex               pre-test questionnaires, quiz Form A or B
  post_form_a.tex  post_form_b.tex              post-test questionnaires, quiz Form A or B
  key_form_a.tex   key_form_b.tex               answer keys with the rationale for every item
  common/                                       parts shared by the questionnaires
  Makefile                                      builds the PDFs
data/
  survey_results.xlsx                           transcribed responses of both waves
notebooks/
  paper-plots.ipynb                             analysis: all figures, tables and numbers of the paper
```

### tasks

The planning document of the lab, which describes the learning objectives, the harness components the
students build, and the schedule of the three weeks.

### survey

The LaTeX sources and PDFs of the questionnaires. The four student forms combine the shared parts in
`common/`: the cover page with the consent, the pseudonymous pairing code, Part A, Part B, and the quiz.
The answer keys are built from the same quiz sources as the student forms and additionally show the correct
answer and the rationale for each item. `common/deprecated_items.tex` archives quiz items that were retired
during the development of the instrument; none of the questionnaires uses them.

To rebuild the PDFs, a TeX Live installation with `latexmk` and the `exam`, `booktabs`, `needspace` and
`tikz` packages is required:

```bash
cd survey
make all        # all six PDFs
make student    # only the four questionnaires
make keys       # only the two answer keys
make clean      # remove build artefacts
```

### data

`survey_results.xlsx` contains the responses transcribed from the paper forms. Students are identified only
by their pseudonymous code. The workbook has three sheets:

- **Data**: one row per student, with the raw responses of both waves side by side.
- **Codebook**: the variables with their labels, value labels and scoring rules.
- **Instructions**: the rules that were used to transcribe the paper forms.

The workbook contains only raw responses. Scores and other derived values are computed in the notebook.

### notebooks

`paper-plots.ipynb` reads the survey data and creates all figures, tables and numbers that are reported in
the paper. The figures are written to `figures/` and the LaTeX tables to `tables/`.

## Running the analysis

The notebook was tested with Python 3.10. To set up an environment and execute the notebook:

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/jupyter nbconvert --to notebook --execute --inplace notebooks/paper-plots.ipynb
```
