   
   <template lang="">
       <div class="row" v-if="showForm">
           <div class="col-md-6 mx-auto">
                <AddCourse @add="addCourse($event)"/>
           </div>
       </div>   

       <div class="row">
           <div class="col-md-6">
                
            <nav aria-label="breadcrumb">
                <slot></slot>
            </nav>
                
               <h1>La liste des cours</h1>
           </div>
           <div class="col-md-6 text-right mt-3">
              
                <button 
                    @click="displayForm" 
                    class="btn btn-sm"
                    :class="{ 'btn-success': !showForm, 'btn-dark': showForm }"
                    >
                        {{ showForm ? 'Fermer' : 'Ajouter cours' }} 
                </button>

           </div>
       </div>

       <div class="row">
           <div class="col-md-4" v-for="course in courses">
               
                <OneCourse :course="course" @delete="deleteOneCourse($event)"/>
               
           </div>
       </div>

     <teleport to='#alert' v-if="courseDeleted">
         <div class="alert alert-danger text-center">
             <strong>Le cours a été suprimé avec succés </strong>
         </div>
     </teleport>

     <teleport to='#alert' v-if="courseAdded">
        <div class="alert alert-success text-center">
            <strong>Le cours à été ajouté avec succés</strong>
        </div>
    </teleport>

   </template>

   <script>
       import OneCourse from './OneCourse'
       import AddCourse from './AddCourse'
   export default {
       components: {
        OneCourse,
        AddCourse
       },
       data() {
           return {
               courseDeleted: false,
               courseAdded: false,
               showForm: false,
               courses: [
                   {
                      id: 1,
                      title: "Apprendre ReactJS",
                      category: 'Framework',
                      tags: [],
                      image: "data:image/jpeg;base64,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"
                   },
                   {
                      id: 2,
                      title: "Apprendre Angular",
                      category: 'Framework',
                      tags: [],
                      image: "https://th.bing.com/th/id/OIP.NYKjH_P64VycUqo7RE-AYgHaD3?pid=ImgDet&rs=1"
                   },
                   {
                      id: 3,
                      title: "Apprendre Javascript",
                      category: 'Framework',
                      tags: [],
                      image: "https://th.bing.com/th/id/R.dfd98e3018d47ec2be1cbf6351bbf533?rik=%2bo82xSHwhvj3rw&pid=ImgRaw&r=0"
                   },
                   {
                      id: 4,
                      title: "Apprendre NodeJS",
                      category: 'Framework',
                      tags: [],
                      image: "https://th.bing.com/th/id/OIP.zmD1GmaHU73rdS_Ox5EcpAHaFj?w=224&h=180&c=7&o=5&dpr=1.25&pid=1.7"
                   },
                   {
                      id: 5,
                      title: "Apprendre Vue",
                      category: 'Framework',
                      tags: [],
                      image: "data:image/jpeg;base64,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"
                   },
                   {
                      id: 6,
                      title: "Apprendre django",
                      category: 'Framework',
                      tags: [],
                      image: "https://th.bing.com/th/id/OIP.KULW5gdtwhuV-FM2onnslwHaEK?w=290&h=180&c=7&o=5&dpr=1.25&pid=1.7"
                   }
               ]
           }
       },
       methods: {
        deleteOneCourse(id) {
            this.courses = this.courses.filter(course => course.id != id)
            this.courseDeleted = true;
            setTimeout(() => { this.courseDeleted = false }, 3000)
        },
        addCourse(course) {
            this.courses = [...this.courses, course];
            this.showForm = false;
            this.courseAdded = true;
            setTimeout(() => { this.courseAdded = false }, 3000)
        },
        displayForm() {
            this.showForm = !this.showForm;
        }
       }
   }
   </script>

   <style scoped>
      h1 {
          color: #ffc107;
      }
   </style>