pipeline {
    agent any
    stages {
        stage('Upload File') {
            steps {
                script {
                    // Mengambil nilai parameter dari input Jenkins
                    def FILE = params.FILE
                    def FILE_NAME = params.FILE_NAME
                    def DEST_FILE = "file/coba" // Modifikasi untuk menetapkan direktori DEST_FILE
                    
                    // Periksa apakah nilai parameter telah diberikan
                    if (FILE && FILE_NAME) { // Tidak perlu memeriksa DEST_FILE karena sudah ditentukan di atas
                        // Ambil ekstensi file yang diunggah
                        def EXTENSION = sh(script: "echo \${FILE##*.}", returnStdout: true).trim()
                        
                        // Ganti nama file sesuai dengan FILE_NAME
                        def NEW_FILE_NAME = "${FILE_NAME}.${EXTENSION}"
                        
                        // Pindahkan file ke DEST_FILE dengan nama yang baru
                        sh "mv $FILE ${DEST_FILE}/${NEW_FILE_NAME}"
                        
                        // Beritahu Jenkins bahwa operasi telah selesai
                        echo "File berhasil diunggah dan disimpan di ${DEST_FILE}/${NEW_FILE_NAME}"
                    } else {
                        error "Usage: FILE and FILE_NAME are required parameters" // Menghapus DEST_FILE dari pesan kesalahan karena sudah ditentukan di atas
                    }
                }
            }
        }
    }
}
