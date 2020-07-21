# PlasSuite-Docker

Two files for building a docker and running the PlasSuite workflow and a sample data described in this [web site](https://github.com/pegi3s/dockerfiles/tree/master/plasflow/1.1.0)   

### PlasSuite dockfile: all programs for running PlasSuite (the size of the docker is then around 8 Gb)

Built your docker from this docker file:
```
docker build -t plassuite -f PlasSuite .
```
Launch this docker as follow:
```
docker run -v /<your home>:/mnt -it plassuite /bin/bash PlasSuite/PlasPredict/PlasPredict.sh and the parameters
```
If you want access to all the file systems of your computer, type then `-v /:/mnt` and all your files will be available in the path `/mnt/<all files in the computer>`.

With the test_data in your home:

```
docker run -v /<your home>:/mnt -it plassuite /bin/bash PlasSuite/PlasPredict/PlasPredict.sh -a /mnt/<path in your home>/test_data/Citrobacter_freundii_strain_CAV1321_scaffolds.fasta -o /mnt/<path in your home>/test_results/PlasPredict --all_db /mnt/<path in your home>/plasmidome_databases --prefix citrobacter
docker run -v /<your home>:/mnt -it plassuite /bin/bash PlasSuite/PlasAnnot/PlasAnnot.sh -f /mnt/<path in your home>/test_results/PlasPredict/citrobacter.predicted_plasmids.fasta -o /mnt/home/debroas/Plasmidome/PlasSuite-Docker/test_results/PlasAnnot --all_db /mnt/<path in your home>/plasmidome_databases
docker run -v /<your home>:/mnt -it plassuite /bin/bash PlasSuite/PlasTaxo/PlasTaxo.sh --predicted_plasmids_dir /mnt/<path in your home>/test_results/PlasPredict -o /mnt/<path in your home>/test_results/PlasTaxo --all_db /mnt/<path in your home>/plasmidome_databases/ --prefix citrobacter --predicted_plasmids_prefix citrobacter 
```

### PlasSuiteWithDatabase dockfile: all programs for running PlasSuite with databases (the size of the docker is then around 115 Gb)

Built your docker from this docker file
```
docker build -t plassuite -f PlasSuiteWithDatabase .
```

With this configuration, the path of the database is not mandatory (the default home is then the root home included in the docker image):
```
docker run -v /<path in your home>:/mnt -it plassuite /bin/bash PlasSuite/PlasPredict/PlasPredict.sh -a /mnt/<path in your home>/test_data/Citrobacter_freundii_strain_CAV1321_scaffolds.fasta -o /mnt/<path in your home>/test_results/PlasPredict --prefix citrobacter
```
