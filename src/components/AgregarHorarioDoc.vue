<template>
  <div>
      <div id="content">
            <div class="">
                <button type="button" id="sidebarCollapse" class=" boton-menu">
                    <i class="fas fa-align-left"></i>
                    <span>Menú</span>
                </button>
            </div>
            <div class="contenido">
                <div class="row">
                    <div class="col-lg-3 ">
                        <form class="formularioElegir">
                            <div class="form-group">
                              <label for="exampleImputFecha">Fecha</label>
                              <input type="text" class="form-control" id="exampleImputFecha" aria-describedby="emailHelp" placeholder="Enter email">
                            </div>
                            <div class="form-group ">
                                <label for="inputIni">Hora de inicio</label>
                                <select id="inputIni" class="form-control">
                                    <option selected>-- Elegir --</option>
                                    <option>08:00</option>
                                    <option>09:00</option>
                                    <option>10:00</option>
                                    <option>11:00</option>
                                    <option>continuara</option>
                                </select>
                            </div>
                            <div class="form-group ">
                                <label for="inputFin">Hora de fin</label>
                                <select id="inputFin" class="form-control">
                                    <option selected>-- Elegir --</option>
                                    <option>09.00</option>
                                    <option>10:00</option>
                                    <option>11:00</option>
                                    <option>12:00</option>
                                    <option>continuara</option>
                                </select>
                            </div>
                            <div class="text-center">
                                <button type="submit" class="btn btn-primary">Submit</button>
                            </div>
                            
                          </form>
                    </div>
                    <div class="col-lg-8">
                        <div class="calendar">

                        </div>
                    </div>
                </div>





            </div>
        </div>
  </div>
</template>

<script>
export default {
    name: 'AgregarHorarioDoc',
    mounted(){
        $('#sidebarCollapse').on('click', function () {
        $('#sidebar, #content').toggleClass('active');
        $('.collapse.in').toggleClass('in');
        $('a[aria-expanded=true]').attr('aria-expanded', 'false');
        });
    }
}
</script>

<style scoped>

/*HORARIO CSS */
.formularioElegir{
    padding: 10px 20px;
    border: 2px solid #f4f4f4;
    background: #f4f4f4;
    margin-left: 20px;
    margin-bottom: 10px;
    
}

.calendar{
    border: 5px solid black;
    width: 100%;
    height: 580px;
    margin-bottom: 20px;
}
/*content */

@import "https://fonts.googleapis.com/css?family=Poppins:300,400,500,600,700";
p {
    font-family: 'Poppins', sans-serif;
    font-size: 1.1em;
    font-weight: 300;
    line-height: 1.7em;
    
}

#sidebar ul li a,
a:hover,
a:focus {
    color: inherit;
    text-decoration: none;
    transition: all 0.3s;
}

.boton-menu {
    cursor: pointer;
    position: relative;
    background: #fff;
    height: 50px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    border-radius: 30px;
    outline: none !important;
    border: none;
    margin-bottom: 15px;
    
}

.line {
    width: 100%;
    height: 1px;
    border-bottom: 1px dashed black;
    margin: 40px 0;
}


/* ---------------------------------------------------
    CONTENT STYLE
----------------------------------------------------- */
#content{
    width: calc(100% - 150px);
    padding: 10px 0 0 0px;
    min-height: 100vh;
    transition: all 0.3s;
    position: absolute;
    top: 0;
    right: 0;
}

#content.active {
    width: 100%;
}

#content .contenido{
    position: relative;
    top:10px;
}

/* ---------------------------------------------------
    MEDIAQUERIES
----------------------------------------------------- */

@media (max-width: 768px) {
    #sidebar {
        margin-left: -150px;
    }
    #sidebar.active {
        margin-left: 0;
    }
    #content {
        width: 100%;
    }
    #content.active {
        width: calc(100% - 150px);
    }
    #sidebarCollapse span {
        display: none;
    }


    .boton-menu {
        cursor: pointer;
        background: #fff;
        height: 50px;
        width: 50px;
        box-shadow: 0 0 6px rgba(0, 0, 0, 0.5);
        border-radius: 30px;
        outline: none !important;
        border: none;
        margin-bottom: 15px;
        
    }
    
}

@media (max-width:375px){
    #sidebar {
        margin-left: -150px;
        
    }
    #sidebar.active {
        margin-left: 0;
        
    }
    #content {
        width: 100%;
    }
    #content.active {
        width: 99%;
    }
    #sidebarCollapse span {
        display: none;
    }

    .boton-menu{
        float:right;
        margin-right: -5px;
    }
    .contenido{
        position: relative;
        margin-top: 30px;
    }

}

</style>