all: Results/knitr_report.html plots_and_reports

plots_and_reports : Plots/pca_plot.tiff Results/correlation_phenotypes_pca.txt

Plots/pca_plot.tiff : Scripts/plot_pca.R
		Rscript --no-save --no-restore --verbose Scripts/plot_pca.R

Results/correlation_phenotypes_pca.txt : Scripts/correlate_with_pca.R
		Rscript --no-save --no-restore --verbose Scripts/correlate_with_pca.R

Results/knitr_report.html: Temp/bmiq_dataset.RData Temp/preprocessed_dataset.RData Temp/dataset_loaded.RData Temp/combat_results.RData Results/analyzed_dataset.RData
		Rscript --no-save --no-restore --verbose Scripts/generate_knitr_report.R

Temp/dataset_loaded.RData: RawData/input_file.txt Scripts/loading.R
		Rscript --no-save --no-restore --verbose Scripts/loading.R

Temp/preprocessed_dataset.RData: Temp/dataset_loaded.RData Configs/probe_filtering.yaml Configs/analysis_samples.txt Configs/normalization.yaml Scripts/preprocessing.R
		Rscript --no-save --no-restore --verbose Scripts/preprocessing.R

Temp/bmiq_dataset.RData: Temp/preprocessed_dataset.RData Configs/bmiq.yaml Scripts/bmiq.R
		Rscript --no-save --no-restore --verbose Scripts/bmiq.R

Temp/combat_results.RData: Temp/bmiq_dataset.RData Scripts/combat.R Configs/combat.yaml
		Rscript --no-save --no-restore --verbose Scripts/combat.R

Results/analyzed_dataset.RData: Temp/combat_results.RData Configs/analysis.yaml Scripts/analysis.R
		Rscript --no-save --no-restore --verbose Scripts/analysis.R
