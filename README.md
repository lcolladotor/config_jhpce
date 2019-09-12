# bashrc_jhpce
My `~/.bashrc` file at JHPCE


```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
	. /etc/bashrc
fi

# User specific aliases and functions
# Auto-complete command from history
# http://lindesk.com/2009/04/customize-terminal-configuration-setting-bash-cli-power-user/
export INPUTRC=~/.inputrc
# http://www.biostat.jhsph.edu/~afisher/ComputingClub/webfiles/KasperHansenPres/IntermediateUnix.pdf
# https://unix.stackexchange.com/questions/48713/how-can-i-remove-duplicates-in-my-bash-history-preserving-order
export HISTCONTROL=ignoreboth:erasedups
export HISTSIZE=20000
shopt -s histappend
shopt -s cmdhist

# http://superuser.com/questions/384769/alias-rm-rm-i-considered-harmful
alias rmi='rm -i'

# Change command prompt
# http://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html
# http://www.cyberciti.biz/faq/bash-shell-change-the-color-of-my-shell-prompt-under-linux-or-unix/
# https://bbs.archlinux.org/viewtopic.php?id=48910
# previous in enigma2: "[\u@\h \W]\$ "
# previously in mac: "\h:\W \u\$ "
export PS1="\[\e[0;33m\]\A \W \$ \[\e[m\]"

# ascp (Aspera Connect) http://downloads.asperasoft.com/en/downloads/8?list
#export PATH=~/.aspera/connect/bin/:$PATH

# Amber2 scracth space (not backed up) for file storage.
alias amber2="cd /legacy/amber2/scratch/lcollado/"

# Brain data results by Alyssa
alias brain="cd /legacy/amber2/scratch/jleek/orbFrontal/results/"
alias stanley="cd /dcs01/stanley/work/brain_rna/"

# LIDB BRAIN projects
alias libd="cd /legacy/nexsan2/disk3/ajaffe/RNASeq/BRAIN/"
alias dersold="cd /dcs01/ajaffe/Brain/derRuns/"
alias ders="cd /dcl01/lieber/ajaffe/derRuns/"
alias jaffe="cd /dcl01/lieber/ajaffe"
alias labold="cd /dcl01/lieber/ajaffe/lab"
alias lab="cd /dcl01/ajaffe/data/lab"
alias emily="cd /dcl01/lieber/ajaffe/Emily"
alias rna="cd /dcl01/lieber/ajaffe/Emily/RNAseq-pipeline/sh"

## RNA-seq mapping bias
#alias mapbias="cd /dcs01/ajaffe/mapBias"

## Leekgroup luster dir
alias leek="cd /dcl01/leek/data/"
alias recount="cd /dcl01/leek/data/recount-website"
alias recounta="cd /dcl01/leek/data/recount-analyses"
alias recount2="cd /dcl01/leek/data/gtex_work/runs/recount2"

## Pandey's recount resoults
alias pandey="cd /dcl01/leek/data/recount_pandey"
alias panday-raw="cd /dcl01/leek/data/sunghee_analysis/processed"

## Creating modules
# https://lmod.readthedocs.io/en/latest/050_lua_modulefiles.html
alias modsrc="cd /jhpce/shared/jhpce/libd"
alias modlua="cd /jhpce/shared/jhpce/modulefiles/libd"

# colors
# http://norbauer.com/notebooks/code/notes/ls-colors-and-terminal-app
# used BSD pattern ExGxFxDxBxEgEdxbxgxhxd on http://geoff.greer.fm/lscolors/
# that tool does not specify the colors, which I did by looking manually at
# http://blog.twistedcode.org/2008/04/lscolors-explained.html
# and the norbauer.com site previously mentioned
alias ls="ls --color=auto"
#export LS_COLORS="di=1;34;40:ln=1;36;40:so=1;35;40:pi=1;93;40:ex=1;31;40:bd=1;34;46:cd=1;34;43:su=0;41:sg=0;46:tw=0;47:ow=0;43"
## After switching to RStudio:
# https://askubuntu.com/questions/466198/how-do-i-change-the-color-for-directories-with-ls-in-the-console
export LS_COLORS="di=0;32:ln=0;36:so=0;35:pi=0;93:ex=0;31:bd=0;34;46:cd=0;34;43:su=0;41:sg=0;46:tw=0;47:ow=0;43:fi=0;33"

# Uncomment below for Mac and comment the two previous commands
#export CLICOLOR=1
#export LSCOLORS="ExGxFxDxBxEgEdxbxgxhxd"

## Python
#export PYTHONPATH="/users/lcollado/.local/lib/python2.7/site-packages/"
#export PYTHONPATH=/users/lcollado/python/python2.7.9:/jhpce/shared/community/compiler/gcc/4.4.7/python/2.7.9/lib/python2.7
#export PATH=/users/lcollado/software/localpython/bin:$PATH

## change dir automatically when using qrsh
## Details: https://github.com/rkostadi/BiocHopkins/wiki/Useless-Tips-&-Code-Snippets
if [ -f ~/.bash_pwd ]; then
    source ~/.bash_pwd
    rm ~/.bash_pwd
fi
alias qr='echo "cd $PWD" > ~/.bash_pwd; history -w; qrsh'
#alias qr='export LEODIR=`pwd`; history -w && qrsh -ac LEODIR'
#alias qr='echo "hola"'

## For setup:
# http://erniemiller.org/2011/12/12/textmate-2-rmate-awesome/
## For laptop config:
# http://jonsimpson.co.uk/log/2011/rmate-ssh-remoteforward
## rmate port
# https://github.com/textmate/rmate
export RMATE_PORT="_a_five_digit_number_"

## For remotes::install_github()
export GITHUB_PAT="something_here"

## Load the git module by default when qrsh/qsub
## thanks to Jiong Yang
if [[ $HOSTNAME == compute-* ]]; then
    echo "Adding LIBD modules"a
    module use /jhpce/shared/jhpce/modulefiles/libd
    echo "Loading git"
    module load git
    module load git-status-size/github
    # module load git-lfs/2.8.0
    module load rmate/1.5.9
    module load conda_R/3.6
fi

## To deal with running nextflow without requesting much more memory
## https://jhpce.jhu.edu/question/why-do-i-get-memory-errors-when-running-java/
export _JAVA_OPTIONS="-Xms5g -Xmx6g"

```

My `~/.input_rc` file:

```bash
#Page up/page down
"\e[B": history-search-forward
"\e[A": history-search-backward

$include /etc/inputrc

```

My `~/.sge_request` file:

```bash
# Check http://www.biostat.jhsph.edu/bit/cluster-usage.html for more instructions
#
# Set defaults for mem_free and h_vmem
-l mem_free=12G,h_vmem=12G
#
# Set the standard value for stack size limit
# (needed for some programs to run properly when h_vmem is set)
-l h_stack=512M
#
# Set a default maximum file size that an SGE job can create
-l h_fsize=100G
# Define my email
-M fellgernon@gmail.com
# To get an email on a job use -m e

```
