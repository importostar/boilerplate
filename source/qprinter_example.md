---
title: qprinter_example
date: 2020-05-07
---
Example Python program qprinter_example.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtGui import QTextDocument
* from PyQt5.QtPrintSupport import QPrinter
* from PyQt5.QtWidgets import QApplication
* import sys

## Methods

* def markdown():

## Code

Example Python PyQt program :

    # Converts Markdown (via pygments) to pdf using Qt5's QPrinter class
    
    from PyQt5.QtGui import QTextDocument
    from PyQt5.QtPrintSupport import QPrinter
    from PyQt5.QtWidgets import QApplication
    
    import sys
    
    someMarkdownText = """
    ## Ille pulsa
    
    Ante trita ignaroque foret turbine tenet. Aequos hunc scribit
    [cibis](http://iuris.org/poenae), non resilit cornua non regia sonat scitarier
    volentem quis. [Agitabitur](http://est.com/et) pudori! Sed brevissimus aperti
    erat cornu pressit humani vitiantes.
    
        software_iso.hypermedia_bios(slaMountPlagiarism, day + snapshot -
                media_function);
        if (skyscraper) {
            lionKoffice(technology);
            virtual = repository.booleanHoverOspf(module);
        } else {
            cloud_camera_upnp = saasSubnetMedia(-3, bps_vram_rfid, tftMidi +
                    dvdEnginePage);
            token.pim -= server;
            buffer_plug.joystick_shell(53);
        }
        if (framework_virtualization + expansion.sli_heuristic_cpm(5 +
                pageMirrorCamera, fsb)) {
            crossDaemonParallel *= 1 + lifo_mtu_tiger;
            table_reimage(domain_network, diskPortalCopy + modem_cluster_ieee,
                    syncVci);
            class.codec_toggle_jfs = -5 / 2 - pipeline_virus_visual;
        }
    
    ## Distabat Quid
    
    Pereo semine fugit haec optastis, subitis si vestibus, est! Hos ferro facti,
    date cursu, Cerberus nequiquam tetigit et fratres. Quodcumque ut aures ignibus
    pro carcere dumosaque vidi aquis videns Quid nimium **concava**, moderato.
    Inpietate amplexus ictu!
    
    ## Rapto post ausim
    
    *Deus suae totas*, hoc arguitur fixo me canam: abest? Liber ademptae, me murmur
    Peleus quo ad Apollinis censu: cornua. In summo percusso claudit! Plus quod
    praeter cernit tu sociosque se modo mons restant sunt levi duobus adspicit, ad.
    Quo a ante trepidum cape quidem altique colla.
    
    Novitasque Hectora canum Haedis; concilio ut medium sequentes accendit? Obstaret
    quae! Gramina lustratum timui **hausitque potuisse** illo aliisque inde.
    """
    
    
    def markdown():
        app = QApplication(sys.argv)
    
        # Set paths
        path = r""".\markdown\markdown.html"""
        outputFile = r""".\markdown\markdownOut.pdf"""
    
        with open(path, "r") as fp:
            html = fp.read()
            
        doc = QTextDocument()
        doc.setHtml(html)
    
        printer = QPrinter()
        printer.setOutputFileName(outputFile)
        printer.setOutputFormat(QPrinter.PdfFormat)
        printer.setDocName("Test")
        printer.setCreator("MSc")
        printer.setPageSize(QPrinter.A4)
        printer.setPageMargins(15, 15, 15, 15, QPrinter.Millimeter)
    
        doc.print(printer)
        print("Done printing.")
    
    
    if __name__ == "__main__":
        markdown()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
