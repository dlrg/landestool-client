<template>
    <section class="container-fluid">
        <div class="animated fadeIn">
          <form @submit.prevent="save">
            <div class="row">
                <div class="col-12">
                    <h1>Timetable</h1>
                    
                    <div class="card">
                        <div class="card-header">
                            <i class="ca ca-anchor"></i> Anwesenheit an den Tagen
                            <button class="btn btn-sm btn-info c-white float-right" type="submit">Speichern</button>
                        </div>
                        <div class="card-body">
                            <div class="form-group row">
                                <h4 class="col-4">Tag</h4>
                                <h4 class="col-3">von</h4>
                                <h4 class="col-3">bis</h4>
                                <div class="col-2"></div>
                            </div>
                            <div class="form-group row" v-for="(item, index) in user.time" :key="'time'+index">
                                <div class="select-wrapper col-xl-4 mb-3">
                                    <select class="form-control  float-left" id="timeDay" v-model="item.day" required>
                                        <option value="Montag">Montag</option>
                                        <option value="Dienstag">Dienstag</option>
                                        <option value="Mittwoch">Mittwoch</option>
                                        <option value="Donnerstag">Donnerstag</option>
                                        <option value="Freitag">Freitag</option>
                                        <option value="Samstag">Samstag</option>
                                        <option value="Sonntag">Sonntag</option>
                                    </select>
                                </div>
                                <div class="select-wrapper col-xl-3 mb-3">
                                    <!--select-time from="14" to="17" :time="item.start"></select-time-->
                                    <select class="form-control  float-left" id="timeStart" v-model="item.start" required>
                                        <option value="8:00">8:00</option>
                                        <option value="9:00">9:00</option>
                                        <option value="10:00">10:00</option>
                                        <option value="11:00">11:00</option>
                                        <option value="12:00">12:00</option>
                                        <option value="13:00">13:00</option>
                                        <option value="14:00">14:00</option>
                                        <option value="15:00">15:00</option>
                                        <option value="16:00">16:00</option>
                                        <option value="17:00">17:00</option>
                                        <option value="18:00">18:00</option>
                                        <option value="19:00">19:00</option>
                                        <option value="20:00">20:00</option>
                                        <option value="21:00">21:00</option>
                                        <option value="22:00">22:00</option>
                                    </select>
                                </div>
                                <div class="select-wrapper col-xl-3 mb-3">
                                    <select class="form-control  float-left" id="timeEnd" v-model="item.end" required>
                                        <option value="8:00">8:00</option>
                                        <option value="9:00">9:00</option>
                                        <option value="10:00">10:00</option>
                                        <option value="11:00">11:00</option>
                                        <option value="12:00">12:00</option>
                                        <option value="13:00">13:00</option>
                                        <option value="14:00">14:00</option>
                                        <option value="15:00">15:00</option>
                                        <option value="16:00">16:00</option>
                                        <option value="17:00">17:00</option>
                                        <option value="18:00">18:00</option>
                                        <option value="19:00">19:00</option>
                                        <option value="20:00">20:00</option>
                                        <option value="21:00">21:00</option>
                                        <option value="22:00">22:00</option>
                                    </select>
                                </div>
                                <div class="delete-button col-xl-1 offset-xl-1">
                                  <button class="btn btn-sm btn-danger float-right" @click.stop="remove(index)">Löschen</button>
                                </div>
                            </div>
                            <button type="button" class="btn btn-sm btn-success ml-1" v-on:click="addForm()">Tag hinzufügen</button>
                         </div>
                      </div>
                    </div>
                </div>
          </form>  
        </div>
    </section>
</template>

<script>
  export default {
    computed: {
      user () {
        return this.$store.getters['user/get'](this.$route.params.userId)
      }
    },
    methods: {
      save () {
        this.$store.dispatch('user/patch', [this.user._id, this.user])
        this.$router.push('/admin/users/' + this.user._id + '/timetable')
      },
      remove (index) {
        this.user.time.splice(index, 1)
      },
      addForm () {
        this.user.time.push({})
      }
    },
    async fetch ({ store, params }) {
      await store.dispatch('user/get', params.userId)
    }
  }
</script>
