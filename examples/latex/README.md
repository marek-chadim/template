This directory has example scripts that illustrate how to use the GentzkowLabTemplate with LaTeX.

See the Examples section of the [template instructions](https://github.com/gentzkow/GentzkowLabTemplate/wiki#examples) for the general procedure for using example scripts.

### List of files

* `my_project_slides.tex` is an example file for slides.
* `my_project.tex` is an example file for a paper, and `my_project.bib` is the associated BibTeX file.

### Steps to set up the LaTeX example for building **slides** with Beamer

1. Place `my_project_slides.tex` in `3_slides/source/`
2. Replace these lines in `3_slides/make.sh`
  
    ```
    #source "${REPO_ROOT}/lib/shell/run_xxx.sh"
    ```
    ```
    # run_xxx my_script.xx "${LOGFILE}"
    ```

    with

    ```
    source "${REPO_ROOT}/lib/shell/run_latex.sh"
    ```
    ```
    run_latex my_project_slides.tex "${LOGFILE}"
    ```

### Steps to set up the LaTeX example for building a **paper**

1. Place `my_project.tex` and `my_project.bib` in `4_paper/source/`
2. Replace these lines in `4_paper/make.sh`
  
    ```
    #source "${REPO_ROOT}/lib/shell/run_xxx.sh"
    ```
    ```
    # run_xxx my_script.xx "${LOGFILE}"
    ```

    with

    ```
    source "${REPO_ROOT}/lib/shell/run_latex.sh"
    ```
    ```
    run_latex my_project.tex "${LOGFILE}"
    ```
3. The example paper `my_project.tex` requires that three input files -- `figure_city.jpg`, `figure_hwy.jpg`, and `table_reg.tex` -- be placed in `/4_paper/input/`. If you set up the example scripts for R, Python, and/or Stata, these files will be created in `2_analysis/output`. You can then have them copied to `/4_paper/input` by replacing this line in `4_paper/make.sh`

    ```
    # cp my_source_files "${MAKE_SCRIPT_DIR}/input/"
    ```

    with
  
    ```
    cp "${REPO_ROOT}/2_analysis/output/"*.jpg "${MAKE_SCRIPT_DIR}/input/"
    cp "${REPO_ROOT}/2_analysis/output/"*.tex "${MAKE_SCRIPT_DIR}/input/"
    ```

    Copying the input files from the output of `2_analysis` is the way the template is designed to be used. But if you want to see how to build the paper without setting up the anlaysis scripts, you can copy the inputs directly from the `/examples/inputs_for_examples/` directory by replacing the above line with

    ```
    cp "${REPO_ROOT}/examples/inputs_for_examples/"*.jpg "${MAKE_SCRIPT_DIR}/input/"
    cp "${REPO_ROOT}/examples/inputs_for_examples/"*.tex "${MAKE_SCRIPT_DIR}/input/"
    ```