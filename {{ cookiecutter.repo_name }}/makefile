rule ?= all		# run rule all by default, which is the default behavior anyway
restart ?= 0	# by default do not restart failed jobs
SHELL := /bin/bash	# allows the running of modules

dry:
	module load Python/3.6.0 R/3.4.2 
	snakemake -p -n $(rule)
srun:
	module load Python/3.6.0 R/3.4.2 
	srun -t 7-0 snakemake --restart-times $(restart) -j 500 -p --max-jobs-per-second 1  --cluster-config cluster.json --cluster "sbatch -p {cluster.partition} --cpus-per-task {threads} -t {resources.time} --mem {resources.mem}G" --rerun-incomplete --notemp --nolock --use-conda $(rule) 
rmout: 
	rm -f *.out
rmdone:
	grep -r -l -Z 'Finished job ' *.out | xargs -0 rm
run:
	snakemake --restart-times $(restart) -j 500 -p --max-jobs-per-second 1  --cluster-config cluster.json --cluster "sbatch -p {cluster.partition} --cpus-per-task {threads} -t {resources.time} --mem {resources.mem}G"     --rerun-incomplete --notemp --nolock --use-conda $(rule)
