# Load libraries
library(shiny)
library(shinydashboard)
library(plotly)

# Sample data (you should replace this with your actual data)
# Assuming you have a data frame named 'swift_data'
# with columns: Date, Album, Song, Value
set.seed(123)
swift_data <- data.frame(
  Date = seq(as.Date("2022-01-01"), as.Date("2022-01-10"), by = "days"),
  Album = rep(c("Album1", "Album2"), each = 5),
  Song = rep(c("SongA", "SongB"), times = 5),
  Value = rnorm(10)
)

# Define UI
ui <- dashboardPage(
  dashboardHeader(title = "Taylor Swift Dashboard"),
  dashboardSidebar(
    sidebarMenu(
      menuItem("The Swift Curve", tabName = "swift_curve", icon = icon("line-chart"),
               menuSubItem("The Swift Curve", tabName = "swift_curve"),
               menuSubItem("By Album", tabName = "by_album"),
               menuSubItem("By Song", tabName = "by_song")
      )
    )
  ),
  dashboardBody(
    tabItems(
      # The Swift Curve tab
      tabItem(tabName = "swift_curve",
              fluidRow(
                box(
                  title = "Introduction",
                  status = "info",
                  solidHeader = TRUE,
                  width = 12,
                  "This is the introduction for The Swift Curve."
                ),
                box(
                  title = "Time Series Plot",
                  status = "primary",
                  solidHeader = TRUE,
                  width = 12,
                  plotlyOutput("swift_curve_plot")
                )
              )
      ),
      
      # By Album tab
      tabItem(tabName = "by_album",
              fluidRow(
                box(
                  title = "Select Album",
                  status = "info",
                  solidHeader = TRUE,
                  width = 12,
                  selectInput("album_selector", "Choose Album:", choices = unique(swift_data$Album)),
                  plotlyOutput("by_album_plot")
                )
              )
      ),
      
      # By Song tab
      tabItem(tabName = "by_song",
              fluidRow(
                box(
                  title = "Select Album and Song",
                  status = "info",
                  solidHeader = TRUE,
                  width = 12,
                  selectInput("album_selector_song", "Choose Album:", choices = unique(swift_data$Album)),
                  selectInput("song_selector", "Choose Song:", choices = unique(swift_data$Song)),
                  plotlyOutput("by_song_plot")
                )
              )
      )
    )
  )
)

# Define server logic
server <- function(input, output) {
  # The Swift Curve plot
  output$swift_curve_plot <- renderPlotly({
    # Your code for The Swift Curve plot using plotly
    # For example:
    plot_ly(data = swift_data, x = ~Date, y = ~Value, type = 'scatter', mode = 'lines')
  })
  
  # By Album plot
  output$by_album_plot <- renderPlotly({
    # Your code for By Album plot using plotly
    # For example:
    filtered_data <- swift_data[swift_data$Album == input$album_selector, ]
    plot_ly(data = filtered_data, x = ~Date, y = ~Value, type = 'scatter', mode = 'lines')
  })
  
  # By Song plot
  output$by_song_plot <- renderPlotly({
    # Your code for By Song plot using plotly
    # For example:
    filtered_data <- swift_data[swift_data$Album == input$album_selector_song & swift_data$Song == input$song_selector, ]
    plot_ly(data = filtered_data, x = ~Date, y = ~Value, type = 'scatter', mode = 'lines')
  })
}

# Run the application
shinyApp(ui, server)
