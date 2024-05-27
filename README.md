
# Manual de proyecto de investigación Herramientas Bioinformáticas

### Nazaret Porras, Nicole Rojas, Alexander Monge, Crista Montiel y Daniela Montero

### Nuestro proyecto se enfoca en la comparación de los proteomas de tres especies de Fusarium con una serie de proteínas relacionadas con la producción del metabolito de albufungina. El objetivo es identificar proteínas ortólogas entre las tres especies.

## Especies a utilizar por su potencial para producir metabolitos antifouling incluyen: Fusarium Solani, Fusarium oxysporum y Fusarium fujikuroi

### Metodología

#### Acceso a Kabré

```bash
ssh -X curso-763@kabre.cenat.ac.cr
Cree un directorio para el proyecto
bash
Copiar código
mkdir proyecto_fungico
Dentro del directorio del proyecto, cree una carpeta para almacenar los proteomas fúngicos
bash
Copiar código
mkdir proyecto_fungico/proteomas
Cambiar al directorio del proyecto
bash
Copiar código
cd proyecto_fungico
Cambia al directorio de proteomas
bash
Copiar código
cd proyecto_fungico/proteomas
Descarga los proteomas desde NCBI
bash
Copiar código
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/013/085/055/GCA_013085055.1_ASM1308505v1/GCA_013085055.1_ASM1308505v1_protein.faa.gz -O Fusarium_graminearum_proteins.faa.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/020/744/495/GCA_020744495.1_Fusso1/GCA_020744495.1_Fusso1_protein.faa.gz -O Fusarium_oxysporum_proteins.faa.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/079/805/GCA_900079805.1_Fusarium_fujikuroi_IMI58289_V2/GCA_900079805.1_Fusarium_fujikuroi_IMI58289_V2_protein.faa.gz -O Fusarium_fujikuroi_proteins.faa.gz
Descomprime los archivos descargados
bash
Copiar código
gunzip *.faa.gz
Cambia los nombres de los archivos para mayor claridad
bash
Copiar código
mv GCA_013085055.1_ASM1308505v1_protein.faa Fusarium_graminearum_proteins.faa
mv GCA_020744495.1_Fusso1_protein.faa Fusarium_oxysporum_proteins.faa
mv GCA_900079805.1_Fusarium_fujikuroi_IMI58289_V2_protein.faa Fusarium_fujikuroi_proteins.faa
Descargue la base de datos Prote_albofungina.fasta
En una nueva ventana me dirijo a la terminal local

Cambiar al directorio donde se encuentra Prote_albofungina.fasta en tu computadora local
bash
Copiar código
cd Desktop
Ejecutar para copiar Prote_albofungina.fasta al servidor remoto en la carpeta Proteomas_proyecto
bash
Copiar código
scp -r Prote_albofungina.fasta curso-763@kabre.cenat.ac.cr:/home/curso-763/Proyecto_final/Proteomas_proyecto/
Regreso a la terminal de Kabré y verifico si en la carpeta Proteomas_proyecto se encuentra mi base de datos
bash
Copiar código
ls /home/curso-763/Proyecto_final/Proteomas_proyecto/
Creación del archivo SLURM: orthofinder.slurm utilizando un editor de texto plano
bash
Copiar código
#!/bin/bash
#SBATCH --job-name=orthofinder_proyecto
#SBATCH --output=orthof_proyecto
#SBATCH --ntasks=4
#SBATCH --time=70:00:00
#SBATCH --partition=dribe

module load miniconda/3
module load miniconda/orthofinder

orthofinder -f Proteomas_proyecto/ -t 20 -M msa -T fasttree
Descargue mi documento de SLURM orthofinder.slurm
En una nueva ventana me dirijo a la terminal local

Cambiar al directorio donde se encuentra orthofinder.slurm en tu computadora local
bash
Copiar código
cd Desktop
Ejecutar para copiar orthofinder.slurm al servidor remoto en la carpeta de Proyecto_final
bash
Copiar código
scp -r orthofinder.slurm curso-763@kabre.cenat.ac.cr:/home/curso-763/Proyecto_final/
Regreso a la terminal de Kabré y verificar si en la carpeta Proyecto_final se encuentra mi documento de SLURM
bash
Copiar código
ls /home/curso-763/Proyecto_final
Para revisar el script SLURM, utiliza el comando less seguido del nombre del archivo
bash
Copiar código
less orthofinder.slurm
Una vez que hayas revisado el script y estés listo para ejecutarlo, utiliza el comando sbatch seguido del nombre del archivo SLURM
bash
Copiar código
sbatch orthofinder.slurm
Una vez que hayas revisado el script y estés listo para ejecutarlo, utiliza el comando sbatch seguido del nombre del archivo SLURM
bash
Copiar código
queue <numero_de_trabajo># Bioinfo
