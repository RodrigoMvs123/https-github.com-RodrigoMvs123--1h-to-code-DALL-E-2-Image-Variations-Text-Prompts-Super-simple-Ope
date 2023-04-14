# https-github.com-RodrigoMvs123--1h-to-code-DALL-E-2-Image-Variations-Text-Prompts-Super-simple-Ope

1h to code DALL-E 2! Image Variations + Text Prompts (Super simple!) | OpenAI API React Node.js

https://www.youtube.com/watch?v=PVK4_foBnwY



https://nodejs.org/en

aniakubow@Anias-MacBook-Pro ~ % cd WebStormProjects
aniakubow@Anias-MacBook-Pro WebStormProjects % npx create-react-app react-dalle-clone-openai

index.js 
import React from ‘react’
import ReactDOM from ‘react-dom/client’
import ‘./index.css’
import App from ‘./App’

const root = ReactDOM.createRoot(document.getElement.Id(‘root’))
root render (
   <React.Strict.Mode>
          <App/>
   </React.Strict.Mode>
)


App.js
import { useState } from “react” 
import Modal from “./components/modal”

const App = () => {
const [ images, setImages ] = useState(null) 
const [value, setValue] = useState(null)
const [error, setError] = useState(null)
const [selectImages, setSelectedImages] = useState(null) 
const [modalOpen, setModalOpen ] = useState(false)  
const surpriseOptions = [
     ‘A blue ostrich eating melon’,
     ‘A matisse style shark on the telephone’,
     ‘A pineapple sunbathing on an island’
]

const = supriseMe = () => {
      const = randomValue = surpriseOptions [Math.floor(Math.random() * surpriseOptions.length)]
      setValue(radomValue)
}

const getImages = async() => {
           setImages(null)
           if value === (null) {
               setError(‘Error must have a search term’)
           return
}
      try {
           const options = {
                   method: “POST”,
                   body: JSON.stringify ({ 
                   message: value
                   }),
                   headers: {
                          “Content-type”: “application/json”
      }
}
           const response = await fetch(‘http://localhost:8000/images’, options)
           const data = await response.json()
           console.log = data
           setImages(data)
    } catch (error) {
          console.error(error)
    }
}


           const uploadImage = async (e) => {
                     console.log(e.target.files[0])
                     
                     const formData = new formData() 
                     formData.append(‘file’, e.target.files[0])
                     setModalOpen(true)
                     setSelectedImage(e.target.files[0])
                     e.target.value = null                    
                     try {
                         const options = {
                         method: “POST”, 
                         body: formData 
}
                         const response = await fetch(‘http://localhost:8000/upload’, options )           
                         const data = await response.json()   
                         console.log(data)
} catch (error) {
        console.error(error)
}
}

 const generateVariations = async () => {
   setImages(null)
   if (selectedImage === null) {
          setError(‘Error ! Must have an existing image ’)
          setModalOpen(false) 
          return 
}
   try {
          const options = {
                method: ‘POST’
}
          const response = await fetch(‘http://localhost:8000/variations’, options)
          const data = await response.json()
          cosole.log(data)
          setImages(data)
          setError(null)
          setModalOpen(false)
} catch (error) {
       console.error(error)
}      
}
     return (
         <div className=”app”>
            <section className”search-section”>
                    <p>Start with a detailed description 
                       <span className”surprise” onClick={surpriseMe}>Surprise me</span>
                    </p>
                  <div className”input-container”
                        <input 
                            value={value}
                            placeholder=”An impressionist oil 
                            painting of a sunflower in a purple vase… ”/>
                            onChange={e => setValue e => setValue (e.target.value) } 
                        <button onClick={getImages}>Generate<button/>
                  </div>
                     <p classeName={“extra-info”}>Or, 
                            <spam> 
                                 <label htmlFor=”files”> upload an image </label>
                                    <input onChange={uploadImage} id=”file” accept=”img /*” type=”file” hidden/>
                            </spam>
                              to edit.
                       </p>
                     {error && <p>{error}</p>}
                     {modalOpen && <div className=”overlay”>}
                         <Modal 
                             setModalOpen={setModalOpen} 
                             setSelectedImage={setSelectedImage} 
                             selectImage={selectedtImage}
                             generateVariations={generateVariations}/>
                     </div>
              </section>
            <section className”image-section”>
                 {Images?.map ((image, _index) => 
                 <img key={_index src={image.url} alt={‘ Generated image of ${value}’}/>
))}  
            </section>
         </div>
)
}

export default App

-https://platform.openai.com/docs/api-reference/images/create-variation

index.css
* {
     font-family: sans-serif;
     
}


body {
    margin: 0;
    padding: 0;
    width: 100vw;
    height: 100vh;
    background-color: #fafafc;
    color: #777;
    display: flex;
    justify-content: center;
}

p {
     font-weight: 200;
     font-size: 14px;
     
}

.app {
    width: 90vw;
    
}

.search-section {
     width:100%;
     display: flex;
     flex-direction: column;
     justify-content: center;
     height: 200%;
}

.surprise {
      background-color: #ececf1;
      color: #000;
      border-radius: 5px;
      font-weight: 600;
      padding: 4px 12px;
      margin: 0 0 2px 5px;
}

.input-container {
      width: 100%;
      display: flex;
      border-radius: 6px;
      overflow: hidden;
      box-shadow: rgba(0, 0, 82, 0.15) 0 2px 4px ;
      
}

.input-container input {
      border: none;
      padding: 13px 14px;
      box-sizing: border-box;
      font-size: 15px;
      outline: none;
      width: 90%;
      font-weight: 200;
}

.input-container input::placeholder {
      color: #cacaca;
      font-weight: 200;
}

.input-container button {
      width: 10%;
      border: none;
      border-left: 1px #cacaca solid;
      background-color: #fff;
      color: #777;
      font-weight: bold;
      cursor: pointer;
}

.input-container button:active {
      background-color: #cacaca;
} 

.image-section{
      width: 100%;
      display:flex;
      flex: wrap: wrap;
      align-items: stretch;
      justify-content: space-between; 
}

.img-section img {
       margin: 1px;
       min-width: 250px;
       max-width: 33%;
       flex-grow: 1;
       
}

@media (max-width: 556px); {
        .img-section img {
              max-width: 100%;
   }
}
        
.extra-info {
         text-align: center;
}

.overlay {
         position: absolute;
         top: 0; 
         left: 0;
         width: 100vw;
         height: 100vh;
         background-color: rgba(0,0,0,0.15);
         overflow: hidden;
         display: flex;
         justify-content: center;
         align-items: center;
         z-index: 10;
}

.modal {
         position: relative;
         z-index: 100;
         background-color: #fff;
         padding: 10px;
         border-radius: 10px;
         display: flex;
         flex-direction: column;
}

.modal.button {
          width: 100%;
          padding: 20px; 
          border: none;
          background-color: #fff;
          cursor: pointer;
}

.modal.button:active: {
          background-color: #fafafc;
}

.img-container {
          height: 256px;
          width: 256px;
          overflow: hidden;
}

aniakubow@Anias-MacBook-Pro ~ % cd WebStormProjects
aniakubow@Anias-MacBook-Pro WebStormProjects % cd react–dalle-clone-openai
aniakubow@Anias-MacBook-Pro WebStormProjects % npm run start

localhost:3000

https://i2symbol.com/abc-123/x


server.js
const PORT = 8000 
const express = require(‘express’)
const cors = require(‘cors’)
const app = express()
app.use (cors()) 
app.use (express.json())
require(‘dotenv’).config()
const { Configuration, OpenAIApi } = require("openai");
const fs= require(‘fs’)
const multer = require(‘multer’)
const configuration = new Configuration({
        apiKey: process.env.API_KEY
});
const openai = new OpenAIApi(configuration)

const storage = multer.diskStorage ({
       destination = (req, file, cb) => {
       cb(null, ‘public’) 
},

fileName: (req, file, cb) => {
       console.log(‘file’, file) 
       cb (null, Date.now + “-” + file.originalname)
} 
}) 

const upload = multer ({storage: storage}).single(‘file’)
let filePath 

app.post(‘/images’, async (req, res) => {
       try {
             const response = await openai.createImage({
                     prompt: req.body.message,
                     n: 10,
                     size: "1024x1024",
             }) 
             console.log(response.data.data)
             res.send(response.data.data)
} catch (error) {
            console.error(error)
}

})

app.post(“/upload” (req.res) => {
       upload(req, res, (err) => { 
         if ( err instanceof multer Multer.Error) {
              return res.status(500).json(err)
         } else if (err) {
              return res.status(500).json(err) 
}
              filePath = req.file.path
    })
             
})

app.post(‘/variations’, async (req, resp) => {
          try {
                const response = await openai.createImageVariation(
                       fs.createReadStream(filePath),
                       10,
                       "1024x1024"
     )
          res.send(response.data.data)
} catch (error) {
          console.error(error)
     }
})

app.listen(PORT, () => console.log(‘Your server is running on PORT ’ + PORT))



aniakubow@Anias-MacBook-Pro react-dalle-clone-openai % npm i express cors dotenv openai fs multer 
https://platform.openai.com/docs/api-reference/images/create?lang=node.js

Terminal 
Local Local(2)
Local(2)
{
url: https://oaida…
Image
},
{
url:
{,

Terminal 
Local Local(2)
Local(2)
path: ‘public/1680698595144-256x256.png’

package.json
“scripts”: {
        “start:frontend”: “react-scripts start”,
}

aniakubow@Anias-MacBook-Pro react-dalle-clone-openai % npm i nodemon

“scripts”: {
        “start:backend”: “nodemon server.js”,
}

aniakubow@Anias-MacBook-Pro react-dalle-clone-openai % npm run start:frontend

aniakubow@Anias-MacBook-Pro react-dalle-clone-openai % npm run start:backend



.env
API_KEY=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


components
Modal.js
import { useState, useRef } from “react”

const Modal = ({ setModalOpen, setSelectedImage, selectedImage, generateVariations }) => { 
     const [ error, setError ] = useState (null)    
     const ref = useRef(null)

     console.log(‘selectedImage’, selectedImage)
     const classModal = () => {
          setModalOpen(false)
          setSelectedImage(null)
}  

     const checkSize = () => {
          if(ref.current.width == 256 && ref.current.height == 256) {
          generateVariations()
  } else {
          setError(‘Error: Choose 256 x 256 image’)
}
     return (
           <div className=”modal”>
               <div onClick={closeModal}>x</div>
                <div className”image-container”>
                        {selectedImage && <img ref = {ref}src={URL.createObjectURL(selectedImage)selectedImage} alt=”uploaded image”/>}
                </div> 
                <p>{error || “* Image must be 256 x 256”} </p>
                { ! error && <button onClick={checkSize}>Generate</button>}
                {error && <button onClick={closeModal}>Close this and try again</button>}
           </div>
    )
}

export default Modal

