<script setup lang="ts">
import { ref, computed } from 'vue'

// Lista dei curriculum disponibili
const curriculumOptions = [
  'Data Science',
  'Cyber-Physical Systems',
  'Software Engineering',
  'Artificial Intelligence'
]

// Lista dei corsi (esempio, da espandere con i 30 corsi effettivi)
const availableCourses = [
  'Machine Learning',
  'Sistemi Distribuiti',
  'Computer Vision',
  'Cloud Computing',
  'Intelligenza Artificiale',
  'Sicurezza Informatica',
  'Ingegneria del Software Avanzata',
  'Big Data',
  'Deep Learning',
  'Internet of Things',
  'Robotica',
  'Human-Computer Interaction',
  'Natural Language Processing',
  'Architetture Software',
  'Metodologie e Tecniche di Test del Software'
]

const studentProfile = ref({
  gender: '',
  age: null,
  residence: '',
  distanceKm: null,
  enrollmentYear: null,
  specialStatus: [],
  academicBackground: {
    degree: '',
    university: ''
  },
  curriculum: '',
  motivation: ''
})

const satisfaction = ref({
  general: 3,
  expectations: '',
  workPreparation: 3,
  organization: 3,
  facilities: 3
})

// Inizializza un corso vuoto come template
const emptyCourse = {
  name: '',
  teacher: '',
  satisfaction: 3,
  relevance: 3,
  wouldChooseAgain: '',
  workload: 3,
  theoryPracticeBalance: 3,
  idealBalance: '',
  applicability: 3,
  courseDescriptionMatch: 3,
  evaluationCoherence: 3,
  materialQuality: 3,
  teacherEvaluation: {
    preparation: 3,
    clarity: 3,
    availability: 3
  },
  suggestions: '',
  bestCurriculum: ''
}

const courses = ref([{ ...emptyCourse }])

const curriculumAnalysis = ref({
  expectedCompetencies: 3,
  missingTopics: '',
  missingUndergraduateCourses: '',
  shortModulesInterest: 3,
  coursesSuggestions: ''
})

const futurePlans = ref({
  intentions: '',
  preparationPerception: 3,
  missingSkills: ''
})

const conclusions = ref({
  additionalFeedback: ''
})

// Metodi
function addCourse() {
  courses.value.push({ ...emptyCourse })
}

function removeCourse(index: number) {
  if (courses.value.length > 1) {
    courses.value.splice(index, 1)
  }
}

function submitSurvey() {
  console.log('Survey submitted:', {
    studentProfile: studentProfile.value,
    satisfaction: satisfaction.value,
    courses: courses.value,
    curriculumAnalysis: curriculumAnalysis.value,
    futurePlans: futurePlans.value,
    conclusions: conclusions.value
  })
  
  // Qui si potrebbe implementare il salvataggio in IndexedDB
  alert('Grazie per aver completato il questionario!')
}
</script>

<template>
  <div class="py-6 space-y-10">
    <div class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h1 class="card-title text-3xl mb-4">Questionario Studenti Magistrale</h1>
        
        <div class="alert alert-info mb-6">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="stroke-current shrink-0 w-6 h-6"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
          <span>Questo questionario è completamente anonimo e ci aiuterà a migliorare l'offerta formativa. Grazie per la tua partecipazione!</span>
        </div>
        
        <!-- Profilo dello studente -->
        <section class="divider divider-primary">Profilo dello Studente</section>
        <div class="space-y-4">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="label">Genere</label>
              <select v-model="studentProfile.gender" class="select select-bordered w-full">
                <option value="">Seleziona</option>
                <option value="m">Maschio</option>
                <option value="f">Femmina</option>
                <option value="altro">Non in Lista</option>
              </select>
            </div>
            
            <div>
              <label class="label">Età</label>
              <input type="number" v-model="studentProfile.age" class="input input-bordered w-full" />
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="label">Provenienza</label>
              <select v-model="studentProfile.residence" class="select select-bordered w-full">
                <option value="">Seleziona</option>
                <option value="in_sede">In sede</option>
                <option value="fuori_sede">Fuori sede</option>
                <option value="pendolare">Pendolare</option>
              </select>
            </div>
            
            <div v-if="studentProfile.residence === 'pendolare'">
              <label class="label">Distanza in km</label>
              <input type="number" v-model="studentProfile.distanceKm" class="input input-bordered w-full" />
            </div>
            
            <div v-else>
              <label class="label">Anno di Iscrizione</label>
              <input type="number" v-model="studentProfile.enrollmentYear" class="input input-bordered w-full" />
            </div>
          </div>
          
          <div>
            <label class="label">Status Particolari (seleziona tutti quelli applicabili)</label>
            <div class="flex flex-wrap gap-2">
              <label class="label cursor-pointer gap-2">
                <input type="checkbox" class="checkbox" value="lavoratore" v-model="studentProfile.specialStatus" />
                <span class="label-text">Lavoratore</span>
              </label>
              <label class="label cursor-pointer gap-2">
                <input type="checkbox" class="checkbox" value="atleta" v-model="studentProfile.specialStatus" />
                <span class="label-text">Atleta</span>
              </label>
              <label class="label cursor-pointer gap-2">
                <input type="checkbox" class="checkbox" value="tempo_parziale" v-model="studentProfile.specialStatus" />
                <span class="label-text">Studente a tempo parziale</span>
              </label>
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="label">Corso di Laurea Triennale</label>
              <input type="text" v-model="studentProfile.academicBackground.degree" class="input input-bordered w-full" />
            </div>
            
            <div>
              <label class="label">Ateneo di Provenienza</label>
              <input type="text" v-model="studentProfile.academicBackground.university" class="input input-bordered w-full" />
            </div>
          </div>
          
          <div>
            <label class="label">Curriculum Scelto</label>
            <select v-model="studentProfile.curriculum" class="select select-bordered w-full">
              <option value="">Seleziona</option>
              <option v-for="curriculum in curriculumOptions" :key="curriculum" :value="curriculum">
                {{ curriculum }}
              </option>
            </select>
          </div>
          
          <div>
            <label class="label">Motivazione Principale della Scelta del Curriculum</label>
            <textarea v-model="studentProfile.motivation" class="textarea textarea-bordered w-full h-24"></textarea>
          </div>
        </div>
        
        <!-- Valutazione complessiva -->
        <section class="divider divider-primary mt-8">Valutazione Complessiva</section>
        <div class="space-y-6">
          <div>
            <label class="label">Soddisfazione Generale per il Curriculum Scelto</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-general" class="mask mask-star-2 bg-orange-400" value="1" v-model="satisfaction.general" />
              <input type="radio" name="rating-general" class="mask mask-star-2 bg-orange-400" value="2" v-model="satisfaction.general" />
              <input type="radio" name="rating-general" class="mask mask-star-2 bg-orange-400" value="3" v-model="satisfaction.general" />
              <input type="radio" name="rating-general" class="mask mask-star-2 bg-orange-400" value="4" v-model="satisfaction.general" />
              <input type="radio" name="rating-general" class="mask mask-star-2 bg-orange-400" value="5" v-model="satisfaction.general" />
            </div>
          </div>
          
          <div>
            <label class="label">Corrispondenza tra Aspettative Iniziali e Realtà del Percorso</label>
            <textarea v-model="satisfaction.expectations" class="textarea textarea-bordered w-full h-24"></textarea>
          </div>
          
          <div>
            <label class="label">Percezione di Preparazione per il Mondo del Lavoro</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-work" class="mask mask-star-2 bg-orange-400" value="1" v-model="satisfaction.workPreparation" />
              <input type="radio" name="rating-work" class="mask mask-star-2 bg-orange-400" value="2" v-model="satisfaction.workPreparation" />
              <input type="radio" name="rating-work" class="mask mask-star-2 bg-orange-400" value="3" v-model="satisfaction.workPreparation" />
              <input type="radio" name="rating-work" class="mask mask-star-2 bg-orange-400" value="4" v-model="satisfaction.workPreparation" />
              <input type="radio" name="rating-work" class="mask mask-star-2 bg-orange-400" value="5" v-model="satisfaction.workPreparation" />
            </div>
          </div>
          
          <div>
            <label class="label">Valutazione dell'Organizzazione Didattica (orari, calendario, distribuzione dei corsi)</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-org" class="mask mask-star-2 bg-orange-400" value="1" v-model="satisfaction.organization" />
              <input type="radio" name="rating-org" class="mask mask-star-2 bg-orange-400" value="2" v-model="satisfaction.organization" />
              <input type="radio" name="rating-org" class="mask mask-star-2 bg-orange-400" value="3" v-model="satisfaction.organization" />
              <input type="radio" name="rating-org" class="mask mask-star-2 bg-orange-400" value="4" v-model="satisfaction.organization" />
              <input type="radio" name="rating-org" class="mask mask-star-2 bg-orange-400" value="5" v-model="satisfaction.organization" />
            </div>
          </div>
          
          <div>
            <label class="label">Valutazione delle Strutture e dei Servizi di Supporto</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-facilities" class="mask mask-star-2 bg-orange-400" value="1" v-model="satisfaction.facilities" />
              <input type="radio" name="rating-facilities" class="mask mask-star-2 bg-orange-400" value="2" v-model="satisfaction.facilities" />
              <input type="radio" name="rating-facilities" class="mask mask-star-2 bg-orange-400" value="3" v-model="satisfaction.facilities" />
              <input type="radio" name="rating-facilities" class="mask mask-star-2 bg-orange-400" value="4" v-model="satisfaction.facilities" />
              <input type="radio" name="rating-facilities" class="mask mask-star-2 bg-orange-400" value="5" v-model="satisfaction.facilities" />
            </div>
          </div>
        </div>
        
        <!-- Valutazione dei corsi -->
        <section class="divider divider-primary mt-8">Valutazione dei Corsi</section>
        <div v-for="(course, index) in courses" :key="index" class="mb-6 p-4 bg-base-200 rounded-box">
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-lg font-semibold">Corso #{{ index + 1 }}</h3>
            <button @click="removeCourse(index)" class="btn btn-sm btn-error" :disabled="courses.length <= 1">
              Rimuovi
            </button>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div>
              <label class="label">Nome del Corso</label>
              <select v-model="course.name" class="select select-bordered w-full">
                <option value="">Seleziona</option>
                <option v-for="c in availableCourses" :key="c" :value="c">{{ c }}</option>
              </select>
            </div>
            
            <div>
              <label class="label">Docente</label>
              <input type="text" v-model="course.teacher" class="input input-bordered w-full" />
            </div>
          </div>
          
          <div class="mb-4">
            <label class="label">Soddisfazione Generale</label>
            <div class="rating rating-lg">
              <input type="radio" :name="`rating-course-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.satisfaction" />
              <input type="radio" :name="`rating-course-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.satisfaction" />
              <input type="radio" :name="`rating-course-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.satisfaction" />
              <input type="radio" :name="`rating-course-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.satisfaction" />
              <input type="radio" :name="`rating-course-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.satisfaction" />
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div>
              <label class="label">Rilevanza Percepita per il Tuo Percorso Formativo</label>
              <div class="rating">
                <input type="radio" :name="`rating-relevance-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.relevance" />
                <input type="radio" :name="`rating-relevance-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.relevance" />
                <input type="radio" :name="`rating-relevance-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.relevance" />
                <input type="radio" :name="`rating-relevance-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.relevance" />
                <input type="radio" :name="`rating-relevance-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.relevance" />
              </div>
            </div>
            
            <div>
              <label class="label">Lo Sceglieresti Nuovamente?</label>
              <div class="flex gap-4">
                <label class="label cursor-pointer">
                  <input type="radio" name="radio-choose-again-{{ index }}" class="radio" value="sì" v-model="course.wouldChooseAgain" />
                  <span class="label-text ml-2">Sì</span>
                </label>
                <label class="label cursor-pointer">
                  <input type="radio" name="radio-choose-again-{{ index }}" class="radio" value="no" v-model="course.wouldChooseAgain" />
                  <span class="label-text ml-2">No</span>
                </label>
                <label class="label cursor-pointer">
                  <input type="radio" name="radio-choose-again-{{ index }}" class="radio" value="non_so" v-model="course.wouldChooseAgain" />
                  <span class="label-text ml-2">Non so</span>
                </label>
              </div>
            </div>
          </div>
          
          <div class="space-y-4">
            <div>
              <label class="label">Adeguatezza del Carico di Lavoro Rispetto ai CFU Assegnati</label>
              <div class="join w-full">
                <span class="join-item btn btn-sm">Insufficiente</span>
                <input type="range" min="1" max="5" v-model="course.workload" class="range range-accent join-item w-full" />
                <span class="join-item btn btn-sm">Eccessivo</span>
              </div>
            </div>
            
            <div>
              <label class="label">Equilibrio tra Teoria e Pratica</label>
              <div class="join w-full">
                <span class="join-item btn btn-sm">Troppa teoria</span>
                <input type="range" min="1" max="5" v-model="course.theoryPracticeBalance" class="range range-accent join-item w-full" />
                <span class="join-item btn btn-sm">Troppa pratica</span>
              </div>
            </div>
            
            <div>
              <label class="label">Equilibrio Ideale tra Teoria e Pratica per Questo Corso</label>
              <textarea v-model="course.idealBalance" class="textarea textarea-bordered w-full"></textarea>
            </div>
            
            <div>
              <label class="label">Applicabilità delle Conoscenze nel Mondo Professionale</label>
              <div class="rating">
                <input type="radio" :name="`rating-applicability-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.applicability" />
                <input type="radio" :name="`rating-applicability-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.applicability" />
                <input type="radio" :name="`rating-applicability-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.applicability" />
                <input type="radio" :name="`rating-applicability-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.applicability" />
                <input type="radio" :name="`rating-applicability-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.applicability" />
              </div>
            </div>
            
            <div>
              <label class="label">Corrispondenza tra Descrizione/Titolo del Corso e Contenuti Effettivi</label>
              <div class="rating">
                <input type="radio" :name="`rating-description-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.courseDescriptionMatch" />
                <input type="radio" :name="`rating-description-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.courseDescriptionMatch" />
                <input type="radio" :name="`rating-description-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.courseDescriptionMatch" />
                <input type="radio" :name="`rating-description-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.courseDescriptionMatch" />
                <input type="radio" :name="`rating-description-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.courseDescriptionMatch" />
              </div>
            </div>
            
            <div>
              <label class="label">Coerenza tra Contenuti del Corso e Modalità di Valutazione</label>
              <div class="rating">
                <input type="radio" :name="`rating-coherence-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.evaluationCoherence" />
                <input type="radio" :name="`rating-coherence-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.evaluationCoherence" />
                <input type="radio" :name="`rating-coherence-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.evaluationCoherence" />
                <input type="radio" :name="`rating-coherence-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.evaluationCoherence" />
                <input type="radio" :name="`rating-coherence-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.evaluationCoherence" />
              </div>
            </div>
            
            <div>
              <label class="label">Qualità del Materiale Didattico</label>
              <div class="rating">
                <input type="radio" :name="`rating-material-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.materialQuality" />
                <input type="radio" :name="`rating-material-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.materialQuality" />
                <input type="radio" :name="`rating-material-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.materialQuality" />
                <input type="radio" :name="`rating-material-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.materialQuality" />
                <input type="radio" :name="`rating-material-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.materialQuality" />
              </div>
            </div>
            
            <div class="border-t pt-4">
              <label class="label font-medium">Valutazione del Docente</label>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div>
                  <label class="label">Preparazione</label>
                  <div class="rating">
                    <input type="radio" :name="`rating-teacher-prep-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.teacherEvaluation.preparation" />
                    <input type="radio" :name="`rating-teacher-prep-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.teacherEvaluation.preparation" />
                    <input type="radio" :name="`rating-teacher-prep-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.teacherEvaluation.preparation" />
                    <input type="radio" :name="`rating-teacher-prep-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.teacherEvaluation.preparation" />
                    <input type="radio" :name="`rating-teacher-prep-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.teacherEvaluation.preparation" />
                  </div>
                </div>
                <div>
                  <label class="label">Chiarezza</label>
                  <div class="rating">
                    <input type="radio" :name="`rating-teacher-clarity-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.teacherEvaluation.clarity" />
                    <input type="radio" :name="`rating-teacher-clarity-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.teacherEvaluation.clarity" />
                    <input type="radio" :name="`rating-teacher-clarity-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.teacherEvaluation.clarity" />
                    <input type="radio" :name="`rating-teacher-clarity-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.teacherEvaluation.clarity" />
                    <input type="radio" :name="`rating-teacher-clarity-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.teacherEvaluation.clarity" />
                  </div>
                </div>
                <div>
                  <label class="label">Disponibilità</label>
                  <div class="rating">
                    <input type="radio" :name="`rating-teacher-avail-${index}`" class="mask mask-star-2 bg-orange-400" value="1" v-model="course.teacherEvaluation.availability" />
                    <input type="radio" :name="`rating-teacher-avail-${index}`" class="mask mask-star-2 bg-orange-400" value="2" v-model="course.teacherEvaluation.availability" />
                    <input type="radio" :name="`rating-teacher-avail-${index}`" class="mask mask-star-2 bg-orange-400" value="3" v-model="course.teacherEvaluation.availability" />
                    <input type="radio" :name="`rating-teacher-avail-${index}`" class="mask mask-star-2 bg-orange-400" value="4" v-model="course.teacherEvaluation.availability" />
                    <input type="radio" :name="`rating-teacher-avail-${index}`" class="mask mask-star-2 bg-orange-400" value="5" v-model="course.teacherEvaluation.availability" />
                  </div>
                </div>
              </div>
            </div>
            
            <div>
              <label class="label">A quale curriculum ritieni che questo corso dovrebbe appartenere?</label>
              <select v-model="course.bestCurriculum" class="select select-bordered w-full">
                <option value="">Seleziona</option>
                <option v-for="curriculum in curriculumOptions" :key="curriculum" :value="curriculum">
                  {{ curriculum }}
                </option>
              </select>
            </div>
            
            <div>
              <label class="label">Suggerimenti per Migliorare il Corso</label>
              <textarea v-model="course.suggestions" class="textarea textarea-bordered w-full h-24"></textarea>
            </div>
          </div>
        </div>
        
        <div class="flex justify-center mt-4">
          <button @click="addCourse" class="btn btn-outline btn-primary">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
            </svg>
            Aggiungi un altro corso
          </button>
        </div>
        
        <!-- Analisi curriculare -->
        <section class="divider divider-primary mt-8">Analisi Curriculare e Suggerimenti</section>
        <div class="space-y-4">
          <div>
            <label class="label">Ritieni che il tuo curriculum ti abbia fornito le competenze che ti aspettavi?</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-curriculum" class="mask mask-star-2 bg-orange-400" value="1" v-model="curriculumAnalysis.expectedCompetencies" />
              <input type="radio" name="rating-curriculum" class="mask mask-star-2 bg-orange-400" value="2" v-model="curriculumAnalysis.expectedCompetencies" />
              <input type="radio" name="rating-curriculum" class="mask mask-star-2 bg-orange-400" value="3" v-model="curriculumAnalysis.expectedCompetencies" />
              <input type="radio" name="rating-curriculum" class="mask mask-star-2 bg-orange-400" value="4" v-model="curriculumAnalysis.expectedCompetencies" />
              <input type="radio" name="rating-curriculum" class="mask mask-star-2 bg-orange-400" value="5" v-model="curriculumAnalysis.expectedCompetencies" />
            </div>
          </div>
          
          <div>
            <label class="label">Quali argomenti vorresti fossero stati approfonditi maggiormente?</label>
            <textarea v-model="curriculumAnalysis.missingTopics" class="textarea textarea-bordered w-full h-24"></textarea>
          </div>
          
          <div>
            <label class="label">Interesse per corsi specifici della triennale non presenti nella magistrale</label>
            <textarea v-model="curriculumAnalysis.missingUndergraduateCourses" class="textarea textarea-bordered w-full"></textarea>
          </div>
          
          <div>
            <label class="label">Interesse per moduli brevi (3 CFU) su competenze tecniche specifiche</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-modules" class="mask mask-star-2 bg-orange-400" value="1" v-model="curriculumAnalysis.shortModulesInterest" />
              <input type="radio" name="rating-modules" class="mask mask-star-2 bg-orange-400" value="2" v-model="curriculumAnalysis.shortModulesInterest" />
              <input type="radio" name="rating-modules" class="mask mask-star-2 bg-orange-400" value="3" v-model="curriculumAnalysis.shortModulesInterest" />
              <input type="radio" name="rating-modules" class="mask mask-star-2 bg-orange-400" value="4" v-model="curriculumAnalysis.shortModulesInterest" />
              <input type="radio" name="rating-modules" class="mask mask-star-2 bg-orange-400" value="5" v-model="curriculumAnalysis.shortModulesInterest" />
            </div>
          </div>
          
          <div>
            <label class="label">Suggerimenti per nuovi corsi o modifiche al curriculum</label>
            <textarea v-model="curriculumAnalysis.coursesSuggestions" class="textarea textarea-bordered w-full h-24"></textarea>
          </div>
        </div>
        
        <!-- Prospettive future -->
        <section class="divider divider-primary mt-8">Prospettive Future</section>
        <div class="space-y-4">
          <div>
            <label class="label">Intenzioni post-laurea</label>
            <select v-model="futurePlans.intentions" class="select select-bordered w-full">
              <option value="">Seleziona</option>
              <option value="lavoro">Lavoro</option>
              <option value="dottorato">Dottorato</option>
              <option value="altro">Altro</option>
            </select>
          </div>
          
          <div>
            <label class="label">Percezione di preparazione rispetto alle richieste del mercato del lavoro</label>
            <div class="rating rating-lg">
              <input type="radio" name="rating-preparation" class="mask mask-star-2 bg-orange-400" value="1" v-model="futurePlans.preparationPerception" />
              <input type="radio" name="rating-preparation" class="mask mask-star-2 bg-orange-400" value="2" v-model="futurePlans.preparationPerception" />
              <input type="radio" name="rating-preparation" class="mask mask-star-2 bg-orange-400" value="3" v-model="futurePlans.preparationPerception" />
              <input type="radio" name="rating-preparation" class="mask mask-star-2 bg-orange-400" value="4" v-model="futurePlans.preparationPerception" />
              <input type="radio" name="rating-preparation" class="mask mask-star-2 bg-orange-400" value="5" v-model="futurePlans.preparationPerception" />
            </div>
          </div>
          
          <div>
            <label class="label">Competenze che ritieni manchino nel tuo percorso formativo</label>
            <textarea v-model="futurePlans.missingSkills" class="textarea textarea-bordered w-full h-24"></textarea>
          </div>
        </div>
        
        <!-- Commenti conclusivi -->
        <section class="divider divider-primary mt-8">Commenti Conclusivi</section>
        <div>
          <label class="label">Feedback aggiuntivi non coperti dalle domande precedenti</label>
          <textarea v-model="conclusions.additionalFeedback" class="textarea textarea-bordered w-full h-32"></textarea>
        </div>
        
        <!-- Pulsante di invio -->
        <div class="flex justify-center mt-8">
          <button @click="submitSurvey" class="btn btn-primary btn-lg">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
            Invia Questionario
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  background-color: hsl(var(--b1) / var(--tw-bg-opacity, 1));
}

.divider-primary {
  font-size: 1.25rem;
  font-weight: 600;
}
</style>