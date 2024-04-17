pipeline {
    agent any
    
    stages {
        stage('Upload File') {
            steps {
                script {
                    // Mengambil nilai parameter dari input Jenkins
                    def FILE = "$FILE"
                    def FILE_NAME = "$FILE_NAME"
                    def DEST_FILE = "$DEST_FILE" // Modifikasi untuk menetapkan direktori DEST_FILE
                    
                    // Periksa apakah nilai parameter telah diberikan
                    if (FILE && FILE_NAME) { // Tidak perlu memeriksa DEST_FILE karena sudah ditentukan di atas
                        // Ambil ekstensi file yang diunggah
                        def EXTENSION = sh(script: "echo \${FILE##*.}", returnStdout: true).trim()
                        
                        // Ganti nama file sesuai dengan FILE_NAME
                        def NEW_FILE_NAME = "${FILE_NAME}.${EXTENSION}"
                        
                        // Pindahkan file ke DEST_FILE dengan nama yang baru
                        sh "mv ${FILE} ${DEST_FILE}/${NEW_FILE_NAME}"
                        
                        // Beritahu Jenkins bahwa operasi telah selesai
                        // Menampilkan informasi setelah operasi mv
                        echo "After mv operation:"
                        sh "ls -lh ${DEST_FILE}"
                        
                        // Menampilkan isi direktori
                        echo "Contents of ${DEST_FILE}:"
                        sh "ls -lh ${DEST_FILE}"
                    } else {
                        error "Usage: FILE and FILE_NAME are required parameters" // Menghapus DEST_FILE dari pesan kesalahan karena sudah ditentukan di atas
                    }
                }
            }
        }
    }
}
