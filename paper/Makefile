# make figures
# make dsc
 
all: $(TEXFILE).pdf $(OUT_FILES) $(CROP_FILES)

figures: figures/egcdf.pdf figures/mean_cdf_nopen.pdf figures/mean_cdf.pdf figures/pi0_est.pdf figures/scenarios_density.pdf
 
dsc: ../dsc-shrink/res.RData ../dsc-robust/dsc_robust.RData ../dsc-robust/summarize_dsc_robust.html ../dsc-shrink/summarize_coverage.html ../dsc-shrink/check_mixfdr_lownoise.html

../dsc-shrink/res.RData:
	cd ../dsc-shrink; R CMD BATCH run_dsc.R
../dsc-robust/dsc_robust.RData:
	cd ../dsc-robust; R CMD BATCH run_dsc_robust.R
../dsc-robust/summarize_dsc_robust.html: ../dsc-robust/dsc_robust.RData
	cd ../dsc-robust; Rscript -e "library(rmarkdown); render('summarize_dsc_robust.rmd')"
../dsc-shrink/summarize_coverage.html: ../dsc-shrink/res.RData
	cd ../dsc-shrink; Rscript -e "library(rmarkdown); render('summarize_coverage.rmd')"
../dsc-shrink/check_mixfdr_lownoise.html:
	cd ../dsc-shrink; Rscript -e "library(rmarkdown); render('check_mixfdr_lownoise.rmd')"

#figures
figures/egcdf.pdf: ../dsc-shrink/res.RData
	cd ../dsc-shrink; R CMD BATCH plot_cdf_eg.R
figures/mean_cdf.pdf: ../dsc-shrink/res.RData
	cd ../dsc-shrink; R CMD BATCH plot_cdf_eg.R
figures/mean_cdf_nopen.pdf: ../dsc-shrink/res.RData
	cd ../dsc-shrink; R CMD BATCH plot_cdf_eg.R
figures/scenarios_density.pdf: ../dsc-shrink/res.RData
	cd ../dsc-shrink; R CMD BATCH plot_egdens.R
figures/pi0_est.pdf: ../dsc-shrink/res.RData
	cd ../dsc-shrink; R CMD BATCH plot_pi0_est.R

 
 
# clean up all files; use with caution
superclean: 
	rm -r ../dsc-shrink/dsc-shrink-files
	rm -r ../dsc-robust/dsc-robust-files
	rm ../dsc-shrink/res.RData
	rm ../dsc-robust/res_robust.RData
	rm figures/*.pdf

 
.PHONY: all figures superclean
