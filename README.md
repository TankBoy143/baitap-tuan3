# baitap-tuan3
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.text.BasicTextField
import androidx.compose.material.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.navigation.NavController
import androidx.navigation.NavGraphBuilder
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            AppNavigation()
        }
    }
}

@Composable
fun AppNavigation() {
    val navController = rememberNavController()
    NavHost(navController = navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        composable("text") { TextDetailScreen() }
        composable("image") { ImageScreen() }
        composable("textfield") { TextFieldScreen() }
        composable("rowlayout") { RowLayoutScreen() }
    }
}

@Composable
fun HomeScreen(navController: NavController) {
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("UI Components List", fontSize = 20.sp, color = Color.Black)
        Spacer(modifier = Modifier.height(8.dp))
        Button(onClick = { navController.navigate("text") }) { Text("Text") }
        Button(onClick = { navController.navigate("image") }) { Text("Image") }
        Button(onClick = { navController.navigate("textfield") }) { Text("TextField") }
        Button(onClick = { navController.navigate("rowlayout") }) { Text("Row Layout") }
    }
}

@Composable
fun TextDetailScreen() {
    Text(
        text = "The quick Brown fox jumps over the lazy dog.",
        fontSize = 24.sp,
        modifier = Modifier.padding(16.dp)
    )
}

@Composable
fun ImageScreen() {
    Column(modifier = Modifier.fillMaxSize().padding(16.dp)) {
        Text("Images")
        Spacer(modifier = Modifier.height(8.dp))
        // Replace with actual image resource or URL loading
        // Image(painter = painterResource(id = R.drawable.sample), contentDescription = null)
        Text("(Hình ảnh mô phỏng ở đây)")
    }
}

@Composable
fun TextFieldScreen() {
    var text by remember { mutableStateOf("") }
    Column(modifier = Modifier.fillMaxSize().padding(16.dp)) {
        Text("Thông tin nhập")
        Spacer(modifier = Modifier.height(8.dp))
        TextField(value = text, onValueChange = { text = it })
    }
}

@Composable
fun RowLayoutScreen() {
    Column(modifier = Modifier.fillMaxSize().padding(16.dp)) {
        Text("Row Layout")
        Spacer(modifier = Modifier.height(8.dp))
        Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.SpaceEvenly) {
            repeat(3) {
                Box(modifier = Modifier.size(50.dp).background(Color.LightGray))
            }
        }
    }
}
