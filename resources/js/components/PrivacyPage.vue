<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 mt-5">
                <form @submit.prevent="save()">
                    <alert-success :form="form">Saved</alert-success>
                    <div class="card">
                        <div class="card-header">
                            <h3 class="card-title">Privacy Policy</h3>

                            <div class="card-tools">
                                <button class="btn btn-app" type="submit">
                                    <i class="fas fa-save"></i> Save
                                </button>
                            </div>
                        </div>
                        <!-- /.card-header -->
                        <div class="card-body p-3">
                            <div class="form-group">
                                <label>Privacy policy text</label>
                                <textarea
                                 v-model="form.privacyText" name="privacyText"
                                    class="form-control"
                                    :class="{ 'is-invalid': form.errors.has('privacyText') }"    
                                rows="20"></textarea>
                                <has-error :form="form" field="privacyText"></has-error>
                            </div>

                            <div class="form-group">
                                <label>Cancelation policy text</label>
                                <textarea
                                 v-model="form.cancelationText" name="cancelationText"
                                    class="form-control"
                                    :class="{ 'is-invalid': form.errors.has('cancelationText') }"    
                                rows="20"></textarea>
                                <has-error :form="form" field="cancelationText"></has-error>
                            </div>
                        </div>
                        <!-- /.card-body -->
                    </div>
                    <!-- /.card -->
                </form>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                form: new Form({
                    page: 'privacy',
                    privacyText: '',
                    cancelationText: '',
                }),
            }
        },
        mounted() {
        },
        created() {
            this.getPage()
        },
        methods: {
            getPage() {
                axios.post('/api/admin/pages', {page: this.form.page})
                    .then(
                        ({
                            data
                        }) => (this.form.fill(data))
                        //
                    )
            },
            save() {
                this.form.post('/api/admin/pages/save')
                    .then(
                        ({
                            data
                        }) => (console.log(data))
                    )
                    .catch(() => {

                    })
            },
        }
    }

</script>
