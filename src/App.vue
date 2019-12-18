<template>
<div id="conteneur">

<table id ="mapage">
<tbody>

<tr>
   <td>
        <h1>
          <label id ="Letitre"></label> 
        </h1>
   </td>
</tr>

<tr>
  <td>  
    <video id="videoco" width="700" height="400" controls autoplay>
      <source id="idvideo" /> 
    </video>
  </td>
</tr>
 
<tr>

  <td>
     <img id ="idimg" width="500" height="600"/>
    
    </td>
</tr>
<tr>
 <td>
<div id="idpara"> </div>
  </td>
</tr>

 

 



<tr>
   <td>
        
          <label id ="authorid"></label> 
     
   </td>
</tr>
<tr>
   <td>

     <label id="date"></label>
   </td>
</tr>




</tbody>
</table>

</div>
</template>



<script>


import axios from 'axios'
export default {
  data(){

    return {Mes_posts:null
  }
    
  },

  
  mounted(){

   
    this.getPosts();
   
  },
  methods: { 

getPosts(){

  axios.get('https://api.meltygroup.com/v1/fr/articles/701166')
        .then(

          response  => { 
          this.Mes_posts = response.data ;
           //récupérer la video 
          var monURL = this.Mes_posts.video.URL.replace("{device}","desktop");
            //récupérer le titre
          var titre = this.Mes_posts.title ;
            //récupérer la photo
          var maphoto = this.Mes_posts.body.items[2].URL.replace("{size}","ajust_1024");
          




     //récupérer l auteur
          var auteur = this.Mes_posts.author.firstname;
              auteur += " "+ this.Mes_posts.author.lastname;

          
          //var mybody = this.Mes_posts.body.URL.replace("{}");
          //alert(maphoto);

             //récupérer le paragraphe 

          var paragraphe = this.Mes_posts.body.items[0].text;
             //récupérer la date 
          var published = this.Mes_posts.body.items[2].date.published;
          
          titre.replace("\u00e9","é");
          
           document.getElementById("idvideo").src = monURL;
           document.getElementById("idvideo").autoplay = "true";
           document.getElementById("videoco").load();

           document.getElementById("Letitre").innerHTML = titre;
           document.getElementById("idimg").src = maphoto;

           
          document.getElementById("authorid").innerHTML=  auteur ;
           
           document.getElementById("date").innerHTML=  published ;

           document.getElementById("idpara").innerHTML= paragraphe;


                     
           
      
          })

}

        
 
  }

} 



</script>

<style>

@media (min-width:768px) and (max-width:1388px)
    
{
    #conteneur{

    width: 100%;
    height:auto;
    margin:auto;
   padding:0; 
    }

    #Letitre
    {
      font-size: 80%;

    }

    #videoco
    {
    
    width: 100%;
    height:auto;
    margin:auto;
    padding: 0;
    }


      #idimg
    {
    
    width: 100%;
    height:auto;
    margin:auto;
    padding: 0;
    }
}
    @media (max-width:767px)
        
        
    {
        
        #conteneur{
    display:block;
    width: 100%;
    padding: 10%;
    height: auto;
    display: inline-block;
    margin: auto ;
    margin-right: 25%;
    margin-left: 35%;
    text-align: center;
    padding: 70px ;
    margin-left: auto;
 
  
        }
          #Letitre
    {
    font-size: 20px;;

    }

    #videoco
    {
    
    width: 100%;
    height: auto;
    padding: 0;
    margin:auto;
    }
    #idimg
    {
    
    width: 100%;
    height: auto;
    padding: 0;
    margin:auto;
    }
    #date
    {
    text-align: center;
    font-size:60%;
    }
  
    
}

body{

    background-color: cornsilk;

}




</style>