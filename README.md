using Oxide.Core.Libraries.Covalence;
using UnityEngine;
using System.Collections.Generic;

namespace Oxide.Plugins
{
    [Info("AntiLootCorpse", "SeuNome", "1.0.0")]
    [Description("Impede que jogadores saqueiem corpos de outros jogadores.")]
    class AntiLootCorpse : CovalencePlugin
    {
        // Hook que detecta quando um jogador tenta saquear algo
        private object CanLootCorpse(Player player, Corpse corpse)
        {
            if (player == null || corpse == null) return null;

            // Verifica se o ID do dono do corpo é diferente do ID de quem está saqueando
            if (corpse.ownerID != player.userID)
            {
                player.ChatMessage("Você não tem permissão para saquear o corpo de outro jogador.");
                return false; // Retorna falso para cancelar a ação de saquear
            }

            return null; // Permite a ação se for o dono
        }

        // Caso queira permitir que membros da mesma equipe saquem, você precisaria
        // adicionar uma verificação de TeamID aqui.
    }
}
