__doxypypy-automation__
=====================================================================================
> __Project:__
> * Creare una pipeline GitLab che utilizzi un immagine docker in grado di analizzare del codice fornito e produrre la documentazione, impaginando poi l'output su una pagina statica seguendo lo standard di doxygen.
>	
>	
> __Tools:__
>
> * doxygen: 
>	produce documentazione analizzando il codice.
> * doxypypy: 
>	traduce la documentazione python ottenuta tramite doxygen in uno standard conforme con quello fornito per gli altri linguaggi.
> * Dockerfile: 
>	documento per la creazione di un immagine che contenga tutto il necessario; python, doxygen, doxypypy.
> - __Instructions:__
>   + install doxygen
>   + install pip
>   + install doxypypy
>   + install doxygen-gui
>   + install graphviz (per le dipendenze di Dot)
>   + crea e sposta py_filter nel $PATH
> ~~~~~~~~~~~~~~~~~~~~~~~{.sh}
> #!/bin/bash
> doxypypy -a -c $1
> ~~~~~~~~~~~~~~~~~~~~~~~
>   + copy doxygen-awesome-css
> ~~~~~~~~~~~~~~~~~~~~~~~{.sh}
> make install
> ~~~~~~~~~~~~~~~~~~~~~~~
>   + use doxygen -g config_file to create doxygen config file
>   + set FILTER_PATTERNS = *.py=py_filter in doxygen config file to run Python code through doxypypy.
>   + use doxygen config_file to generate documentation
> -
> __more at https://www.doxygen.nl/manual/doxygen_usage.html__