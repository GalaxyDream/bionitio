# Overview 

Generate bionitio README.md files based on a template.

This allows us to make sure all the README files for bionitio are consistent, and only differ where necessary due to
language specific differences.

# Example usage

```
bionitio-readme.sh -t TEMPLATE.md -l python -i $HOME/bionitio-python/readme_includes > $HOME/bionitio-python/README.md
```

# How to update all the bionitio READMEs for all the different language implementations

1. Clone all the repositories using the bionitio git wrapper:
```
bs=$BIONITIO_SRC
mkdir $SCRATCH_DIR
cd $SCRATCH_DIR
${bs}/githelper/bionitio-git.sh -c clone
```
Or, if you already have cloned the repositories, then you can pull their updates:
```
${bs}/githelper/bionitio-git.sh -c pull 
```
2. Make your changes to the template `TEMPLATE.md`, or to the implementation-specific files in the `readme_includes` directory in each implementation of bionitio.
3. Run the README template program for each language:
```
for lang in c clojure cpp csharp haskell java js perl5 python r ruby rust; do \
    ${bs}/readme_template/bionitio-readme.sh -t ${bs}/readme_template/TEMPLATE.md -l "$lang" -i "bionitio-${lang}/readme_includes" > "bionitio-${lang}/README.md"; \
done
```
4. Commit the changes with a message:
```
${bs}/githelper/bionitio-git.sh -c commit -m "Put your commit message here"
```
5. Push your changes back to git:
```
${bs}/githelper/bionitio-git.sh -c push
```