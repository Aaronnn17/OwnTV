package tv.own.owntv.player

data class ChannelVariant(
    val channelId: Long, // O el tipo de ID que use la entidad Channel en OwnTV_Core
    val originalName: String,
    val qualityLabel: String, // Ej: "FHD", "HD", "SD", "Opción 2"
    val categoryName: String?,
    val playlistName: String?,
    val streamUrl: String
)

object ChannelVariantHelper {
    private val QUALITY_REGEX = Regex(
        """\b(UHD|4K|FHD|1080p|HD|720p|SD|HEVC|H\.?265|50fps|60fps|RAW|VIP|BACKUP)\b""",
        RegexOption.IGNORE_CASE
    )
    private val PREFIX_REGEX = Regex("""^(\[.*?\]|\(.*?\)|[A-Z]{2,3}\s*[|:\-]\s*)+""")
    private val SYMBOLS_REGEX = Regex("""[^a-zA-Z0-9áéíóúÁÉÍÓÚñÑ]+""")

    /**
     * Obtiene el nombre limpio para comparar ("DAZN LA LIGA FHD" -> "daznlaliga")
     */
    fun getBaseName(rawName: String): String {
        return rawName
            .replace(PREFIX_REGEX, "")
            .replace(QUALITY_REGEX, "")
            .replace(SYMBOLS_REGEX, "")
            .trim()
            .lowercase()
    }

    /**
     * Extrae las etiquetas de calidad para mostrarlas claras en el submenú ("FHD", "HD HEVC", etc.)
     */
    fun extractQualityBadge(rawName: String): String {
        val matches = QUALITY_REGEX.findAll(rawName).map { it.value.uppercase() }.toList()
        return if (matches.isNotEmpty()) matches.joinToString(" · ") else "Estándar"
    }
}
