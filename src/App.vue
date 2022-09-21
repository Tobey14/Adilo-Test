<template>
  <Header />

  <section class="readyDiv" style="height:100%;" v-if="askingPermission">

    <div class="contentuals">
        <i class="fa fa-close topRight"  @click="closeSetUp()"></i>
        <div class="d-flex noti-Div">
            <div class="noti-badge mt-1"></div>
            <h5 class="ml-2 preview">Live Preview</h5>
        </div>
        <div class="blueDiv">

        </div>

        <div class="modal-footer justify-content-center mt-2">
            <button type="button" class="button text-center" style="width: 259px;height: 51px;" @click="startRecording()">Start Recording</button>
        </div>

        
    </div>
  </section>


  <section class="readyDiv" style="height:100%;" v-else-if="recording">

    <div class="contentuals">
        <i class="fa fa-close topRight" @click="closeSetUp()"></i>

        
        <div class="d-flex noti-Div">
            <div class="noti-badge mt-1"></div>
            <h5 class="ml-2 preview">Live Recording</h5>
        </div>
        <div class="blueDiv">
            <video class="video" width="100%" height="100%" controls autoplay></video>
            <audio class="audio" width="100%" height="100%" style="visibility:hidden;" controls autoplay>
              <source class="audioSourceOgg" src="" type="audio/ogg">
              <source class="audioSourceMp3" src="" type="audio/mpeg">
            </audio>
        </div>

        <div class="modal-footer justify-content-center mt-2">
            <button type="button" class="button btnDisabled text-center" style="width: 259px;height: 51px;" @click="startRecording()">Start Recording</button>
            <button type="button" v-if="recording && recordCamera && !recordMic" @click="stopCameraRecord()" class="button text-center" style="width: 259px;height: 51px;background-color:red;color:white;">Stop Recording</button>
            <button type="button" v-if="recording && recordMic && !recordCamera" @click="stopMicRecord()" class="button text-center stopAudioBtn" style="width: 259px;height: 51px;background-color:red;color:white;">Stop Recording</button>
            <button type="button" v-if="recording && recordMic && recordCamera" @click="stopCameraRecord()" class="button text-center stopAudioBtn" style="width: 259px;height: 51px;background-color:red;color:white;">Stop Recording</button>
        </div>

        
    </div>
  </section>

  <section class="content" v-else>
    <div class="row">
      <div class="col-md-2 sidebar">
        <ul class="nav flex-column sideContent">
          <li class="nav-item px-2 mb-4 actif">
            <a class="nav-link" href="#"> <i class="fa fa-film mr-3"></i> My Recordings</a>
          </li>
          <li class="nav-item px-2">
            <a class="nav-link" href="#"><i class="fa fa-share-alt mr-4"></i> Requested</a>
          </li>
        </ul>
      </div>


      <div class="col-md-10">
        <div class="mainContainer">
          <div class="row">
            <ul class="nav">
              <li class="nav-item">
                <a class="nav-link active descTog" href="#">SnapByte</a>
              </li>

              <li class="nav-item">
                <i class="nav-link fa fa-angle-right mt-1 descTog"></i>
              </li>



              <li class="nav-item">
                <a class="nav-link descTog" href="#">My Recordings</a>
              </li>

            </ul>
          </div>

          <div class="row">
            <div class="col-4 desc">
              My Recordings <span class="ml-3">{{recordings.length>0?recordings.length: 0}}</span>
            </div>

            <div class="col-8">
              <ul class="nav float-right">
                <li class="nav-item">
                  <a class="nav-link active button mr-3" href="#" @click="sortByDate()"> <i class="fa fa-arrows-v" style="cursor:pointer" ></i> By Date</a>
                </li>



                <li class="nav-item">
                  <a class="nav-link button mr-3 dropdown-toggle" href="#" id="navbarDropdown" role="button"
                    data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"> <i class="fa fa-filter"></i> Add
                    Filter <i class="fa fa-angle-down"></i></a>
                  <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <a class="dropdown-item activate" href="#" style="cursor:pointer" @click="sortByTitle()">By Title</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="#" style="cursor:pointer" @click="sortByViews()">By Views</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="#" style="cursor:pointer" @click="sortBySize()">By Size</a>
                  </div>
                </li>


                <li class="nav-item">
                  <a class="nav-link button mr-3 btnRequest" href="#"> <i class="fa fa-video-camera"></i> New
                    Request</a>
                </li>


                <li class="nav-item">
                  <a class="nav-link button btnRecord" href="#" data-toggle="modal" data-target="#exampleModalCenter"><i class="fa fa-microphone"></i> Start Recording</a>
                </li>

              </ul>
            </div>
          </div>

          <div class="row">

            <div class="row mt-5 mb-5" v-if="this.recordings.length > 0">
              <table class="table table-borderless table-responsive">
                <thead>
                  <tr>
                    <th scope="col" style="max-width:150px;">Recording</th>
                    <th scope="col" style="min-width:350px;">Title</th>
                    <th scope="col">View</th>
                    <th scope="col">Size</th>
                    <th scope="col">Last Modified</th>
                    <th scope="col"> </th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(rec,index) in recordings" :key="index">

                    <td style="max-width:150px;">

                      <video class="" :srcObject="rec.src" width="120" height="70" controls v-if="rec.type == 'video'">
                        <source :srcObject="rec.src" type="video/mp4">
                        <source :srcObject="rec.src" type="video/ogg">
                      </video>

                      <audio class="audio" style="width:120px !important" controls v-if="rec.type == 'audio'">
                        <source class="" :src="rec.src" type="audio/ogg">
                        <source class="" :src="rec.src" type="audio/mpeg">
                      </audio>

                      <video class="" :src="rec.src" width="120"  height="70" controls v-if="rec.type == 'videoScreen'">
                        <source :src="rec.src" type="video/mp4">
                        <source :src="rec.src" type="video/ogg">
                      </video>
                      <!-- <img src="./assets/images/social-2.png" alt="" class="recThumb"> -->
                    </td>
                    <td>
                      <h5 class="recName">{{rec.project}}</h5>
                      <p class="recDesc"> {{rec.description}}</p>
                    </td>
                    <td class="recViews">{{rec.views}}</td>
                    <td class="recSize">{{rec.size}}</td>
                    <td class="recTime">{{Math.floor((((new Date()) - rec.date).toString())/(1000*60)) }} minutes ago</td>
                    <td class="recDots">
                      <i class="fa fa-circle mr-2 mt-2"></i> <i class="fa fa-circle mr-2 mt-2"></i><i
                        class="fa fa-circle mr-2 mt-2"></i>

                    </td>
                  </tr>

<!-- 
                  <tr>
                    <td style="max-width:150px;">
                      <img src="./assets/images/social-3.png" alt="" class="recThumb">
                    </td>
                    <td>
                      <h5 class="recName">Getting it right the first time</h5>
                      <p class="recDesc"> The Video description is shown here if the user has added it.</p>
                    </td>
                    <td class="recViews">324</td>
                    <td class="recSize">932 KB</td>
                    <td class="recTime">3 months ago</td>
                    <td class="recDots">
                      <i class="fa fa-circle mr-2 mt-2"></i> <i class="fa fa-circle mr-2 mt-2"></i><i
                        class="fa fa-circle mr-2 mt-2"></i>

                    </td>
                  </tr>


                  <tr>
                    <td style="max-width:150px;">
                      <img src="./assets/images/social-4.png" alt="" class="recThumb">
                    </td>
                    <td>
                      <h5 class="recName">Getting it right the first time</h5>
                      <p class="recDesc"> The Video description is shown here if the user has added it.</p>
                    </td>
                    <td class="recViews">324</td>
                    <td class="recSize">932 KB</td>
                    <td class="recTime">3 months ago</td>
                    <td class="recDots">
                      <i class="fa fa-circle mr-2 mt-2"></i> <i class="fa fa-circle mr-2 mt-2"></i><i
                        class="fa fa-circle mr-2 mt-2"></i>

                    </td>
                  </tr> -->

                </tbody>
              </table>
            </div>

            <div class="emptyContent" v-else>
              <div class="text-center">
                <img src="./assets/images/empty-folder.svg" alt="" class="imgEmpty"><br>
                <h3 class="sayHello">Say Hello To The World!</h3>
                <p>Record your first video/audio and share it what your team, friends, followers and customers.</p>

                <div class="d-flex text-center btnDiv">
                  <a class="nav-link button mr-2 btnRecord" href="#" data-toggle="modal" data-target="#exampleModalCenter"><i class="fa fa-microphone"></i> Start
                    Recording</a>

                  <a class="nav-link button btnRequest" href="#"> <i class="fa fa-video-camera"></i> New Request</a>
                </div>


              </div>

            </div>


            
          </div>

          <div class="row mt-5 mb-5 " v-if="this.recordings.length < 1">
            <div class="col-md-6">
              <img src="./assets/images/adilo.jpg" alt="" class="adiloImage">
            </div>

            <div class="col-md-6 d-flex justify-content-center align-items-center">

              <div class="flexContent">
                <h3 class="sayHello">Want more controls & better quality recording?</h3>
                <a class="nav-link button btnRequest mt-4" href="#" style="width:265px;"> Download the desktop
                  recorder</a>

              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    
  </section>

  

  <!-- Modal -->
    <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog"
      aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">New Recording</h5>
            <button type="button" class="close" style="font-size:32px;" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">

            <h5 class="saveIn">Save the recording in</h5>
            <select name="" id="" v-model="selectedProject" @change="projectChanged()">
              <option :value="project" v-for="(project, index) in projects" :key="index">{{project}}</option>
            </select>

            <h5 class="saveIn  mt-3">Enter Description</h5>
            <input type="text" class="descInput px-2" placeholder="Enter Description" v-model="description" id="">

            <div class="d-flex mt-4">
              <h5 class="modalRec">Record screen</h5>
              <label class="switch ml-auto">
                <input type="checkbox" :checked="recordScreen?true: false" @change="toggleRecordScreen()"/>
                <span class="slider round"></span>
              </label>
            </div>

            <div class="d-flex mt-3">
              <h5 class="modalRec">Record camera</h5>
              <label class="switch ml-auto">
                <input type="checkbox" :checked="recordCamera?true: false" @change="toggleRecordCamera()"/>
                <span class="slider round"></span>
              </label>
            </div>

            <div class="d-flex mt-3">
              <h5 class="modalRec">Record mic</h5>
              <label class="switch ml-auto">
                <input type="checkbox" :checked="recordMic?true: false" @change="toggleRecordMic()"/>
                <span class="slider round"></span>
              </label>
            </div>
          </div>
          <div class="modal-footer justify-content-center">
            <button type="button" class="button btnRequest text-center" data-dismiss="modal" aria-label="Close" style="width: 259px;height: 51px;" @click="this.askingPermission = true">Start
              Recording</button>
          </div>
        </div>
      </div>
    </div>
</template>


<script>

import Header from './Header.vue';

export default {
  props: [],
  data() {
    return {
      recordings:[],
      projects:{
        0:'Getting it Right The First Time',
        1:'Peace in my country',
        2: 'Community leaders Have to wake up',
        3: 'We are the best'
      },
      selectedProject:'Getting it Right The First Time',
      askingPermission:false,
      recording:false,
      recordScreen:true,
      recordCamera:false,
      recordMic:false,
      description:'',
      loading:false
    };
  },
  components: {
    Header,
  },
  computed: {

  },
  methods: {
    toggleRecordScreen(){
      this.recordScreen = !this.recordScreen;
      this.updateView();
    },
    toggleRecordCamera(){
      this.recordCamera = !this.recordCamera;
      this.updateView();
    },
    toggleRecordMic(){
      this.recordMic = !this.recordMic;
      this.updateView();
    },

    async recordWithScreen(){

      let stream = await navigator.mediaDevices.getDisplayMedia({
        video: true
      });

      this.askingPermission = false;
      this.recording = true;


      //for better browser support
      const mime = MediaRecorder.isTypeSupported("video/webm; codecs=vp9") 
                ? "video/webm; codecs=vp9" 
             : "video/webm"
      let mediaRecorder = new MediaRecorder(stream, {
          mimeType: mime
      })

      let chunks = []
      mediaRecorder.addEventListener('dataavailable', function(e) {
          chunks.push(e.data);
      })

      mediaRecorder.addEventListener('stop', function(){
          let blob = new Blob(chunks, {
              type: chunks[0].type
          })

          let video = document.querySelector(".video");
          let url = URL.createObjectURL(blob);

          video.src = url;
          sessionStorage.setItem('videoUrl', url);

          
      })
      //start the recorder manually
      mediaRecorder.start()

      

    },

    recordWithCamera(){     
      

      var localStreamConstraints = {
          audio: this.recordMic? true:false,
          video: true,
      };

      this.askingPermission = false;
      this.recording = true;
      
    
      console.log('recording camera');
      

      navigator.mediaDevices
      .getUserMedia(localStreamConstraints)
      .then((stream)=>{
          document.querySelector('.video').srcObject = stream;

          // [...this.recordings, newRecord]; 
          // this.recordings.push(newRecord);
      })
      .catch(function (e) {
          if (confirm("An error with camera occured:(" + e.name + ") Do you want to reload?")) {
              location.reload();
          }
      });

    },

    recordWithScreenAndCamera(){     
      

      var localStreamConstraints = {
          audio: this.recordMic? true:false,
          video: true,
      };

      this.askingPermission = false;
      this.recording = true;
      
    
      console.log('recording camera');
      

      navigator.mediaDevices
      .getUserMedia(localStreamConstraints)
      .then((stream)=>{
          document.querySelector('.video').srcObject = stream;

          this.recordWithScreen().then(()=>{

            setTimeout(()=>{
              var size = Math.floor(Math.random() * 1000);
              var date = new Date();
              const newRec = {type:'videoScreen', src:sessionStorage.getItem('videoUrl'), project:this.selectedProject, description:this.description, views:1, size:size+' KB', date:date};

              this.recordings.push(newRec);

              sessionStorage.removeItem('videoUrl');
              setTimeout(()=>{
                document.querySelector(".video").src = '';

              },10000)

            },6000)


          });

          // [...this.recordings, newRecord]; 
          // this.recordings.push(newRecord);
      })
      .catch(function (e) {
          if (confirm("An error with camera occured:(" + e.name + ") Do you want to reload?")) {
              location.reload();
          }
      });

    },

    stopCameraRecord() {
      this.recording = false;
      let record = document.querySelector('.video').srcObject;
      var size = Math.floor(Math.random() * 1000);
      var date = new Date();
      var newRecord = { type:'video', src:record, project:this.selectedProject, description:this.description, views:1, size:size+' KB', date:date };
      let tracks = record.getTracks();

      this.recordings.push(newRecord);

			tracks.forEach(track => {
				track.stop();
			});
    },

    recordWithMic(){
      console.log('recording mic')
      this.askingPermission = false;
      this.recording = true;

      navigator.mediaDevices.getUserMedia({ audio: true })
      .then(stream => {

       
        const mediaRecorder = new MediaRecorder(stream);
        mediaRecorder.start();
        const audioChunks = [];

        mediaRecorder.addEventListener("dataavailable", event => {
          audioChunks.push(event.data);
        });

        mediaRecorder.addEventListener("stop", () => {
          const audioBlob = new Blob(audioChunks);
          const audioUrl = URL.createObjectURL(audioBlob);
          
          let audioSourceMp3 = document.querySelector('.audioSourceMp3');
          let audioSourceOgg = document.querySelector('.audioSourceOgg');

          audioSourceMp3.src = audioUrl;
          audioSourceOgg.src = audioUrl;
        });

        document.querySelector('.stopAudioBtn').addEventListener('click', function(){
          mediaRecorder.stop();
        })
      })
    },

    stopMicRecord(){
      this.loading=true;
      setTimeout(()=>{
        var url = document.querySelector('.audioSourceMp3').src;
        var size = Math.floor(Math.random() * 1000);
        var date = new Date();
        const newRec = {type:'audio', src:url, project:this.selectedProject, description:this.description, views:1, size:size+' KB', date:date};
        this.recordings.push(newRec);
        sessionStorage.removeItem('audioUrl');

        this.askingPermission = false;
        this.recording = false;
      },2000);


    },

    

    startRecording(){
      this.updateView();
      console.log('yes')

      if((this.recordScreen && this.recordCamera && !this.recordMic) || (this.recordScreen && this.recordCamera && this.recordMic)){
        this.recordWithScreenAndCamera();
      }

      if(this.recordScreen && !this.recordCamera && !this.recordMic){
        this.recordWithScreen().then(()=>{

          setTimeout(()=>{
            var size = Math.floor(Math.random() * 1000);
            var date = new Date();
            const newRec = {type:'videoScreen', src:sessionStorage.getItem('videoUrl'), project:this.selectedProject, description:this.description, views:1, size:size+' KB', date:date};

            this.recordings.push(newRec);

            sessionStorage.removeItem('videoUrl');
            setTimeout(()=>{
              document.querySelector(".video").src = '';

            },10000)

          },6000)


        });
      }

      if((this.recordCamera && !this.recordScreen && !this.recordMic) || (this.recordCamera && this.recordMic)){
        this.recordWithCamera();
      }


      if(this.recordMic && !this.recordCamera && !this.recordScreen){
        this.recordWithMic();
      }

      
    },

    closeSetUp(){
      this.askingPermission = false;
      this.recording = false;

      this.stopCameraRecord();
      this.stopMicRecord();
    }, 
    
    updateView(){

      if(this.recordings.length>0){

        //update views
        this.recordings.forEach((rec)=>{
          var old_views = rec.views;
          var new_views = old_views + 1;
          rec.views = new_views;
        });

        // update time

        // setTimeout(()=>{
                
        //   this.recordings.forEach((rec)=>{
        //     var old_date = rec.date;
        //     var new_date = old_date + 1;
        //     rec.date = new_date;
        //   });
        // })
      }
      
    },


    sortByDate(){
      if(this.recordings.length>1){
        this.recordings.reverse();
      }   
    },
    sortByTitle(){
      this.recordings.sort(this.dynamicSort("project"));
    },
    sortByViews(){
      if(this.recordings.length>1){

        this.recordings.sort(function(a,b) {
          return a.views - b.views;
        }).then((rec)=>{
          this.recordings = rec;
        });
      }
    },
    sortBySize(){

      if(this.recordings.length>1){
        this.recordings.sort(function(a,b) {
          return a.size - b.size;
        }).then((rec)=>{
          this.recordings = rec;
        });
      }
       
    },

    dynamicSort(property) {
      var sortOrder = 1;

      if(property[0] === "-") {
          sortOrder = -1;
          property = property.substr(1);
      }

      return function (a,b) {
          if(sortOrder == -1){
              return b[property].localeCompare(a[property]);
          }else{
              return a[property].localeCompare(b[property]);
          }        
      }
    }
    


  },

  mounted() {

  },
};
</script>



<style scoped>
</style>