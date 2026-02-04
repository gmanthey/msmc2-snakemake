# msmc2-snakemake

## Installation

1. If you haven't yet, install [conda miniforge](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install).

2. Clone this repository, cd into it and download the submodule `msmc-tools`:

    ```bash
    git clone https://github.com/gmanthey/msmc2-snakemake.git
    cd msmc2-snakemake
    git submodule init
    git submodule update
    ```

3. Create a new environment from the environment specs file:
4. 
    ```bash
    conda env create -f environment.yml
    ```

    If the `msmc2-snakemake` environment had been created previously, make sure 
    you update to the newest version using `conda env update --file environment.yml --prune`

## Usage

1. Copy the `config.yml.template` file to `config.yml` 
2. Adjust the paths to the genome fasta, vcf file and aligned bam directory in the `config.yml` file. Adjust the `final_bam_extension` if necessary, the files are expected to follow the following naming convention: `<individual-id><final_bam_extension>.bam`.
3. Create the `resources/chromosomes.txt` file, which should contain one line per chromosome and just the name of the chromosome on the line. This should include only autosomes.
4. With phased data:
   - Create the `resources/populations.txt` file, which should contain one line per population, with the first entry of the line being the population name and all consequent, space-delimited entries being the individual ids. To keep memory usage managable, it is recommended to not include all individuals of a population, 5 individuals per population has proven to be adequate.
   without phased data:
   - Create the `resources/populations.txt` file, which should contain a single line, with the first entry being the name of the population and the second entry (after a space), should be the name of the one individual you want to use. This individual should be as high-quality as possible.
5. Run the workflow:
   ```bash
   snakemake
   ```
   If you are on Uni Oldenburgs rosa cluster, you may use the `--profile profile/default` flag to set command line options to use the slurm system of that cluster.
6. The folder `notebooks` contains a ipynb to plot the result of the calculations.
